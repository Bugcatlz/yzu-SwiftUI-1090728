# HW1
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Image("Pic")
            .resizable()
            .aspectRatio(contentMode: .fill)
            .overlay(
                Text("Good")
                    .fontWeight(.heavy)
                    .lineSpacing(20)
                    .font(.system(size:32.0))
                    .frame(width: 350, height: 150,
                           alignment: .center)
                    .background(Color.blue)
                    .cornerRadius(20, antialiased: true)
                    .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                    .overlay(
                        Image(systemName:"hand.thumbsup")
                            .font(.system(size:40))
                            ,
                        alignment:.leading
                    )
                ,
                alignment: .bottom
            )
            .overlay(
                Text("1090728                                 施承亨")
                    .fontWeight(.heavy)
                    .lineSpacing(20)
                    .font(.system(size:24.0))
                    .frame(width: 350, height: 150,
                           alignment: .center)
                ,
                alignment: .top
            )
    }
}

```

<img src="https://github.com/Bugcatlz/yzu-SwiftUI-1090728/blob/05b0ab8f6eba3cd202af6c5a249335f2ccfab1f3/IMG_1419.jpeg">
