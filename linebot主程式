var LineToken = '你的Token';
var replymessage = [{'type': 'text', 'text':''}];
var SpreadSheet = SpreadsheetApp.openByUrl('你的試算表url');
var SheetName = SpreadSheet.getSheetByName('工作表');

function doPost(e) {
  console.log('info:' + e.postData.contents);
  var value = JSON.parse(e.postData.contents);  
  try {
    var events = value.events;
    if (events != null) {
      for (var i in events) {
        var event = events[i];
        var type = event.type;
        var replyToken = event.replyToken;  // 要回復訊息 reToken
        var sourceType = event.source.type;
        var userId = event.source.userId;   // 取得個人userId
        var groupId = event.source.groupId; // 取得群組Id
        var timeStamp = event.timestamp;
        var displayName = getUsername(userId);
        
        switch (type) {
          case 'message':
            var messageType = event.message.type;
            var messageId = event.message.id;
            var messageText = event.message.text;            // 使用者Message字串
            KeyWord(messageText,replyToken,displayName);     // 關鍵字判斷
            break;
            
          case 'postback':
            var pdata = event.postback.data;
            Postback(pdata,replyToken);
            break;
            
          default:
            break;          
        }
      }
    }
  } catch(ex) {
    console.log(ex);
  }
}

//*******************************發訊息Function****************************
function replyMsg(replyToken, replyMsg, LineToken) {
  var url = 'https://api.line.me/v2/bot/message/reply';
  var opt = {
    'headers': {
    'Content-Type': 'application/json; charset=UTF-8',
    'Authorization': 'Bearer ' + LineToken,
  },
  'method': 'post',
  'payload': JSON.stringify({
    'replyToken': replyToken,
      'messages': replyMsg   //[{'type': 'text', 'text': '哈囉'}]
   })
  };
  UrlFetchApp.fetch(url, opt);
}
function pushMsg(pushMsg, usrId) {
  var url = 'https://api.line.me/v2/bot/message/push';
  var opt = {
    'headers': {
    'Content-Type': 'application/json; charset=UTF-8',
    'Authorization': 'Bearer ' + LineToken,
  },
  'method': 'post',
  'payload': JSON.stringify({
    'to': usrId,
    'messages': pushMsg     //[{'type': 'text', 'text': '哈囉'}]
  })
 };
 UrlFetchApp.fetch(url, opt);
}

//*******************************Line其他功能*******************************
//取得用戶暱稱
function getUsername(userId) {
  var url = 'https://api.line.me/v2/bot/profile/' + userId;
  var response = UrlFetchApp.fetch(url, {
    'headers': {
      'Authorization': 'Bearer ' + LineToken,
    }
  });
  return JSON.parse(response.getContentText()).displayName;
}
