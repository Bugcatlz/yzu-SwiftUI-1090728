# HW2
## 猜拳遊戲

使用者可以在下方選擇剪刀、石頭或布，電腦也會隨機選擇一個種類，並判斷勝負，當獲勝時會播放音效。此外，在最上方會顯示當前的勝利、平手和失敗的次數

---

### 程式碼
```swift
import SwiftUI
import AVFoundation
struct ContentView: View { 
    @State var selectedType:String = ""
    @State var randomType:Int = 0
    @State var selectedPic:String = ""
    @State var randomPic:String = ""
    @State var result:String = ""
    @State var player = AVPlayer()
    @State var winCount = 0
    @State var loseCount = 0
    @State var tieCount = 0
    var body: some View{
        VStack{
            HStack{
                Text(String(winCount) + " - " + String(tieCount))
                    .font(.system(size:30))
                    .fontWeight(.bold)
                Text( " - " + String(loseCount))
                    .font(.system(size:30))
                .fontWeight(.bold)
            }
            Image(randomPic)
                .resizable()
                .scaledToFit()
                .rotationEffect(.degrees(180))
            Text(result)
                .font(.system(size:50))
           Image(selectedPic)
                .resizable()
                .scaledToFit()
            HStack{
                Button(action: {
                    selectedPic = "scissor"
                    randomType = Int.random(in: 0...2)
                    if randomType == 0{
                        randomPic = "scissor"
                        result = "平手"
                        tieCount = tieCount + 1
                    }
                    else if randomType == 1{
                        randomPic = "stone"
                        result = "你輸了！"
                        loseCount = loseCount + 1
                    }
                    else{
                        randomPic = "paper"
                        result = "你贏了！"
                        winCount = winCount + 1
                        let url = Bundle.main.url(forResource: "win", withExtension: "mp3")!
                        let playItem = AVPlayerItem(url:url)
                        player.replaceCurrentItem(with:playItem)
                        player.play()
                    }
                }, label: {
                    Text("剪刀")        
                        .frame(width:100,height:50)
                        .font(.system(size:30))
                        .padding(.all,10)
                        .background(Color.blue)
                        .foregroundColor(.white)
                        .cornerRadius(/*@START_MENU_TOKEN@*/3.0/*@END_MENU_TOKEN@*/)
                })
                Button(action: {
                    selectedPic = "stone"
                    randomType = Int.random(in: 0...2)
                    if randomType == 0{
                        randomPic = "scissor"
                        result = "你贏了！"
                        winCount = winCount + 1
                        let url = Bundle.main.url(forResource: "win", withExtension: "mp3")!
                        let playItem = AVPlayerItem(url:url)
                        player.replaceCurrentItem(with:playItem)
                        player.play()
                    }
                    else if randomType == 1{
                        randomPic = "stone"
                        result = "平手"
                        tieCount = tieCount + 1
                    }
                    else{
                        randomPic = "paper"
                        result = "你輸了！"
                        loseCount = loseCount + 1
                    }
                }, label: {
                    Text("石頭")        
                        .frame(width:100,height:50)
                        .font(.system(size:30))
                        .padding(.all,10)
                        .background(Color.blue)
                        .foregroundColor(.white)
                        .cornerRadius(/*@START_MENU_TOKEN@*/3.0/*@END_MENU_TOKEN@*/)
                })
                Button(action: {
                    selectedPic = "paper"
                    randomType = Int.random(in: 0...2)
                    if randomType == 0{
                        randomPic = "scissor"
                        result = "你贏了！"
                        winCount = winCount + 1
                        let url = Bundle.main.url(forResource: "win", withExtension: "mp3")!
                        let playItem = AVPlayerItem(url:url)
                        player.replaceCurrentItem(with:playItem)
                        player.play()
                    }
                    else if randomType == 1{
                        randomPic = "stone"
                        result = "你輸了！"
                        loseCount = loseCount + 1
                    }
                    else{
                        randomPic = "paper"
                        result = "平手"
                        tieCount = tieCount + 1
                    }
                }, label: {
                    Text("布")        
                        .frame(width:100,height:50)
                        .font(.system(size:30))
                        .padding(.all,10)
                        .background(Color.blue)
                        .foregroundColor(.white)
                        .cornerRadius(/*@START_MENU_TOKEN@*/3.0/*@END_MENU_TOKEN@*/)
                })
            }
        }
    }
    
}

```

### 成果

[影片](https://youtu.be/SGZd7DO-Zmo?si=qnCCjkNavc32Y3s6)
