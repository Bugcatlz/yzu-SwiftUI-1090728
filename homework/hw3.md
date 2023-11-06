# HW3
## 蒐藏庫
---
### 程式碼
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack{
            TitleView()
            HStack{
                AnimalView(imageName: "cat", textSize: 30)
                AnimalView(imageName: "duck", textSize: 30)
                AnimalView(imageName: "sheep", textSize: 30)
            }
            ZStack{
                HStack{
                    AnimalView(imageName: "snake", textSize: 30)
                    AnimalView(imageName: "spider", textSize: 30)
                }
//                SnakeView()
                Text("危險請勿觸碰")
                    .font(.system(size:20))
                    .foregroundColor(.white)
                    .padding(.all,5)
                    .background(Color.red)
                    .opacity(0.7)
                    .offset(x:0,y:0)
              }
            HStack{
                AnimalView(imageName: "bat", textSize: 30)
                AnimalView(imageName: "butterfly", textSize: 25)
                AnimalView(imageName: "turtle", textSize: 30)
            }
            
        }.padding(.all,15)
        
    }
}

struct TitleView: View {
    var body: some View {
        VStack(alignment:.center,spacing:2){
            Text("施承亨的")
                .font(.system(size:30))
            Text("動物園")
                .font(.title)
                .foregroundColor(Color(red:29/255,
                                       green:40/255,blue:192/255))
        }
    }
}

struct AnimalView: View {
    var imageName: String
    var textSize: Int
    var body: some View {
        VStack{
            Image(imageName)
                .resizable()
                .aspectRatio(contentMode:.fit)
                .frame(height:100,
                       alignment: .center)
            Text(imageName.capitalized)
                .fontWeight(.bold)
                .font(.system(size:CGFloat(textSize)))
        }
        .frame(minWidth: 0,idealWidth: 100,
               maxWidth: .infinity, minHeight: 0,
               idealHeight: 100,maxHeight: .infinity,
               alignment: .center)
    }
}


struct SnakeView: View {
    var body: some View {
        VStack{
            Image("snake")
                .resizable()
                .aspectRatio(contentMode:.fit)
                .padding(.all,15)
            Text("Snack")
                .fontWeight(.bold)
                .font(.system(size:30))
        }
    }
}

extension UIScreen{
    static let screenWidth = UIScreen.main.bounds.size.width
    static let screenHeigh = UIScreen.main.bounds.size.height
    static let screenSize = UIScreen.main.bounds.size
}
```
---
### 成果
<img src = "">
