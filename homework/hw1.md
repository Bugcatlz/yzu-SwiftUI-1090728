# HW1
## 一頁式個人檔案
---
### 程式碼

```swift
import SwiftUI

extension Color {
    init(hex: String) {
        let scanner = Scanner(string: hex)
        var rgb: UInt64 = 0
        
        scanner.scanHexInt64(&rgb)
        
        let red = Double((rgb & 0xFF0000) >> 16) / 255.0
        let green = Double((rgb & 0x00FF00) >> 8) / 255.0
        let blue = Double(rgb & 0x0000FF) / 255.0
        
        self.init(red: red, green: green, blue: blue)
    }
}

struct ContentView: View {
    var body: some View {
        ZStack{
            Rectangle()
                .fill(Color(hex:"A6CDE7"))
                .frame(minWidth: /*@START_MENU_TOKEN@*/0/*@END_MENU_TOKEN@*/,idealWidth: 100,maxWidth: .infinity,minHeight: 0,idealHeight: 100,maxHeight: .infinity,alignment: .center)
            VStack{
                Text("個人檔案")
                    .font(.system(size: 50))
                    .bold()
                Image("Pic")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                    .frame(width:300,height:300,alignment: .top)
                    .background(Color.white)
                    .cornerRadius(300.0)
                    .overlay(
                        Circle()
                            .stroke(Color.blue, lineWidth:10)
                    )
                HStack{
                    Text("姓名：施承亨")
                        .font(.system(size: 20))
                        .padding(.all,10)
                    Text("學號：1090728")
                        .font(.system(size: 20))
                        .padding(.all,10)
                }    
                
                HStack{
                    Text("學而時習之，不亦說乎？")
                        .font(.system(size: 25))
                    Image(systemName: "a.book.closed.fill.zh") 
                        .resizable()
                        .frame(width:25,height: 30)
                }
            }
        }
            
    }
}
---
### 成果
```
<img scr="picture/hw1_image.jpg">
<img src="https://github.com/Bugcatlz/yzu-SwiftUI-1090728/blob/05b0ab8f6eba3cd202af6c5a249335f2ccfab1f3/IMG_1419.jpeg">
