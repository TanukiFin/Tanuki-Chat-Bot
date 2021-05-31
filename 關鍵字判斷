/*
  判斷用戶訊息，並給予回覆，執行replyMsg()
*/

function KeyWord(messageText,replyToken,displayName){
  switch(messageText){
    case '暱稱':
      replymessage = [{'type': 'text', 'text': displayName}]; 
      break;
    case '測試':
      replymessage = [{'type': 'text', 'text': '測試成功'}]; 
    default:
      break;       
  } 
  replyMsg(replyToken, replymessage, LineToken);
}
