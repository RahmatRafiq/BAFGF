function importCSVAndSubmitForm() {
  var formId = '19XTLlx932ISm5lQzAGNBOexhzaTFlWhqGK_-7kCEpUQ'; // Ganti dengan ID formulir Anda
  var form = FormApp.openById(formId);

  var csvFileId = '11UGsMwJ3LLAw5O5m4Kse9xGV1OLiDOYA'; // Ganti dengan ID file CSV di Google Drive
  var csvData = DriveApp.getFileById(csvFileId).getBlob().getDataAsString();
  var csvRows = csvData.split('\n');

  var headers = csvRows[0].split(',');

  for (var i = 1; i < csvRows.length; i++) {
    var rowData = csvRows[i].split(',');
    
    var formResponse = form.createResponse();
    var items = form.getItems();

    for (var j = 0; j < headers.length; j++) {
      var answerIndex = parseInt(rowData[j]);
      var questionTitle = headers[j];

      var questionItem = items.filter(item => item.getTitle() === questionTitle)[0];
      if (questionItem) {
        if (questionItem.getType() === FormApp.ItemType.MULTIPLE_CHOICE) {
          var choices = questionItem.asMultipleChoiceItem().getChoices();
          if (answerIndex >= 0 && answerIndex < choices.length) {
            var optionResponse = questionItem.asMultipleChoiceItem().createResponse(choices[answerIndex].getValue()); // Menggunakan nilai pilihan, bukan objek pilihan
            formResponse.withItemResponse(optionResponse);
          }
        } else {
          var textResponse = questionItem.asTextItem().createResponse(rowData[j]);
          formResponse.withItemResponse(textResponse);
        }
      }
    }

    formResponse.submit();
  }
}
