```
.service('SelectPreviewDelete', function() {

  let makeFileSelector = function(dataObject, scope) {
    let fileSelector = function(selector, imageId) {
      let reader = new FileReader();
      reader.onload = function(event) {
        let dataURL = reader.result;
        let image = document.getElementById(imageId);
        image.src = dataURL;
        dataObject.data = dataURL;
        scope.$apply();
      };
      dataObject.fileName = selector.value.split(/(\\|\/)/g).pop();
      let file = selector.files[0];
      reader.readAsDataURL(file);
    };
    return fileSelector;
  };

  let makeFileDeletor = function(dataObject) {
    let fileDeletor = function(selectorId, imageId) {
      let selector = document.getElementById(selectorId);
      selector.value = '';
      let image = document.getElementById(imageId);
      image.src = '';
      dataObject.data = undefined;
      dataObject.fileName = undefined;
    };
    return fileDeletor;
  };

  return {
    makeFileSelector: makeFileSelector,
    makeFileDeletor: makeFileDeletor,
  };

})
```
