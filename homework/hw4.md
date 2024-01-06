# HW4
## 金庸介紹
--
### 程式碼

#### ContentView

````swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Text("金庸介紹")
                .font(.largeTitle)
                .fontWeight(.heavy)
                .foregroundStyle(.primary)
            TabView{
                Group{
                    WelcomeView()
                        .tabItem{
                            Image(systemName: "info.circle")
                            Text("Description")
                        }
                    BookListView()
                        .tabItem{
                            Image(systemName: "list.dash")
                            Text("Books")
                        }
                    CardView()
                        .tabItem { 
                            Image(systemName: "book")
                            Text("Cold Fact")
                        }
                }
                .toolbarBackground(Color.black, for: .tabBar)
                .toolbarBackground(.visible, for: .tabBar)
//                .toolbarColorScheme(.dark, for: .tabBar)    
            }
            .tint(.yellow)
        }.padding(.top,20)
            
    }
}
```

#### WelcomeView
```swiftUI
import SwiftUI

struct WelcomeView:View{
    @AppStorage("UserName") var UserName:String = ""
    var body: some View{
        VStack{
            Image("金庸")
                .resizable()
                .cornerRadius(10, antialiased: /*@START_MENU_TOKEN@*/true/*@END_MENU_TOKEN@*/)
                .aspectRatio(contentMode:.fit)
            Text("查良鏞")
                .font(.system(size: 25))
                .bold()
            Text("以筆名「金庸」創作多部膾炙人口的武俠小說。歷年來金庸筆下的著作屢次改編為電視劇、電影等影視作品，對華人影視文化貢獻重大，奠定他成為華人知名作家的基礎，素有「有華人的地方，就有金庸的武俠」的稱讚。他因優秀的文學作品而被稱為「香港四大才子」之一，與古龍、梁羽生合稱為「中國武俠小說3劍客」。")
                .padding()
                
        }.padding(.top,20)
    }
}
```

#### BookListView
```swiftUI
import SwiftUI

struct Book: Identifiable{
    var id = UUID()
    var image:String
    var bookName:String
    var description:String
    var year:Int
}

var books = [
    Book(image: "射雕英雄傳", bookName: "射雕英雄傳", description: "《射鵰英雄傳》是一部武俠小說，金庸「射鵰三部曲」之第一部，又名《大漠英雄傳》。它的發表確立了金庸「武林至尊」的地位。該小說被多次改編成同名電影、電視連續劇、電玩遊戲。",year: 1957),
    Book(image: "天龍八部", bookName: "天龍八部", description: "《天龍八部》是作家金庸筆下魁宏複雜的一部武俠小說作品。創作初衷以佛教的神話生物象徵，譜寫8個主角，各自成章最後交織為一。連載時逐漸發展成多線敍事、伏筆綿密的群像連續劇，以大理段氏、姑蘇慕容、蕭峯身世為核心，前後達30年的家仇國恨的史詩悲劇。本書橫跨地域廣闊，牽涉民族與個人的深刻情感矛盾。",year:1963),
    Book(image: "神鵰俠侶", bookName: "神鵰俠侶", description: "《神鵰俠侶》是金庸創作的武俠小說，為「射鵰三部曲」的第二部。《神鵰俠侶》在描寫情感方面為金庸作品中著墨最多、最深入的一部，被讀者稱為「情書」，也曾多次被改編為影視作品、動畫、漫畫和廣播劇。",year: 1959),
    Book(image: "倚天屠龍記", bookName: "倚天屠龍記", description: "《倚天屠龍記》為香港作家金庸所著的一部武俠小說，「射鵰三部曲」之一，為其三部曲之最後一部。作為跨越宋元兩個朝代的武俠傳奇故事的結局篇，其他二部包括《射鵰英雄傳》、《神鵰俠侶》是同一個時期的故事，角色也互相熟識；到《倚天屠龍記》主線故事時，已過了快九十年，屬於元末的故事。",year: 1961),
    Book(image: "笑傲江湖", bookName: "笑傲江湖", description: "《笑傲江湖》是金庸創作的武俠小說，最初在新加坡《新明日報》連載，後於1967年4月20日至1969年10月12日連載於《明報》，後結集出版。",year: 1967),
    Book(image: "鹿鼎記", bookName: "鹿鼎記", description: "《鹿鼎記》是香港作家金庸的最後一部武俠小說作品。該小說於1969年至1972年間創作，故事發生在清初。1969年10月24日開始在《明報》連載，到1972年9月23日刊完，一共連載了2年11個月。此書是金庸封筆之作，收錄於《金庸作品集》中。它與《碧血劍》的情節有所關連。",year: 1969)]


struct BookListView: View {
    @State var showDetailView = false;
    @State var selectBook:Book?
    var body: some View {
        NavigationView{
            List(books){
                bookItem in
                BasicBookImageRow(thisBook: bookItem)
                    .onTapGesture {
                        self.showDetailView = true
                        self.selectBook = bookItem
                    }
            }
            .sheet(item:self.$selectBook,content:{
                bookItem in
                BookDetailView(thisBook: bookItem)
            })
            .navigationTitle("著作列表")
        }
    }
}

struct BasicBookImageRow: View{
    var thisBook:Book
    var body: some View{
        HStack{
            Image(thisBook.image)
                .resizable()
                .frame(width:40, height:60)
                .cornerRadius(5, antialiased: /*@START_MENU_TOKEN@*/true/*@END_MENU_TOKEN@*/)
            Text(thisBook.bookName)
            Spacer()
            Text("\(thisBook.year)年")
        }
    }
}

struct BookDetailView:View{
    @Environment(\.presentationMode) var presentationMode
    var thisBook:Book
    var body: some View{
        ScrollView{
            VStack{
                Text(thisBook.bookName)
                    .font(.system(.title,design: .rounded))
                    .fontWeight(.black)
                    .padding()
                Image(thisBook.image)
                    .resizable()
                    .aspectRatio(contentMode:.fill)
                    .clipped()
                    .padding(.bottom)
                Text(thisBook.description)
                    .padding()
                Spacer()
            }    
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName:"chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.black)
                    })
                    .padding(.trailing,20)
                    .padding(.top,20)
                    Spacer()
                }
            })
    }
}
```

#### CardView
```swiftUI
import SwiftUI

var coldFacts = ["金庸原名是查良鏞，他的筆名「金庸」是由他的兩位朋友的名字各取一個字組成的。","金庸是位法學碩士，曾在香港大學法學院任教，但他更喜歡寫武俠小說。","他的作品中，最早發表的是《書劍恩仇錄》，而《笑傲江湖》則被視為他武俠小說創作的巔峰之作。","金庸在他的小說中經常描寫英雄人物，但他自己卻表示對於現實世界的政治不感興趣。","金庸的小說曾多次被改編成電影、電視劇和其他媒體作品，廣受歡迎。"]

struct CardView:View{
    @State var currentCard = Int.random(in: 0..<coldFacts.count)
    var body: some View{
        VStack{
             VStack{
                 Text("冷知識")
                     .font(.title)
                     .bold()
                 Text(coldFacts[currentCard])
                     .font(.body)
                     .foregroundStyle(.black)
                     .padding(.all,10)
             }
             .frame(minWidth: 0,idealWidth: 100,maxWidth: 300,
                    minHeight: 0,idealHeight: 100,maxHeight: 300,alignment: .center)
             .background(Color.yellow)
             .onTapGesture{
                 var nextCard =  Int.random(in: 0..<coldFacts.count)
                  while nextCard == currentCard{
                      nextCard = Int.random(in: 0..<coldFacts.count)
                  }
                 currentCard = nextCard
             }
            Text("點擊查看下一頁")
                .padding(.all,10)
        }
        
    }
}
```
---
###成果
[Demo影片](https://youtu.be/YyHzR8IOKWI?si=NO4Up3UwN5nPKY1N)
