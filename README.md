```
.service('SPUD', function() {

  let make = function(selectorId, imageId, dataObject, scope) {

    let selector = document.getElementById(selectorId);
    let image = document.getElementById(imageId);

    let select = function() {
      let reader = new FileReader();
      reader.onload = function(event) {
        let dataURL = reader.result;
        image.src = dataURL;
        dataObject.data = dataURL;
        scope.$apply();
      };
      dataObject.fileName = selector.value.split(/(\\|\/)/g).pop();
      let file = selector.files[0];
      reader.readAsDataURL(file);
    };

    let discard = function() {
      selector.value = '';
      image.src = '';
      dataObject.data = undefined;
      dataObject.fileName = undefined;
    };

    return {
      select: select,
      discard: discard,
    };

  };

  return {
    make: make,
  };

})
```
