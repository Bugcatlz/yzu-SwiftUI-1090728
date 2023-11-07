## setting
---
### 程式碼
```swift
import SwiftUI

struct ContentView: View {
    let displayFontType = [".default",".rounded",".monospaced",".serif"]
    @State var displayFontSelected = 0
    @State var IsDeepScheme = false
    @State var colorArray:Array = [255.0,255.0]
    @State var stepperValue = 0
    @State var sliderValue = 0.0
    @State var selectedDate = Date()
    
    var body: some View {
        NavigationView{
            Form(content:{
                Section(header: Text("字型設定"),content:{
                    Picker(selection: $displayFontSelected,
                           label: Text("字型選擇(\(displayFontSelected))"),content: {
                        ForEach(0..<displayFontType.count,
                                id:\.self,
                                content:{
                            Text(self.displayFontType[$0])
                        })
                    })
                })
                Section(header: Text("背景風格"),content: {
                    Toggle(isOn: $IsDeepScheme) {
                     Text("深色(\(String(IsDeepScheme)))")
                    }
                })
                Section(header: Text("計數器"),content:{
                    Stepper(
                        onIncrement: {stepperValue+=1},
                        onDecrement: {stepperValue-=1},
                        label: {
                            Text("Stepper(\(stepperValue))")
                        })
                })
                Section(header:Text("滑桿(\(sliderValue,specifier:"%.2f"))")){
                    Slider(value:$sliderValue,in: 0...1 )
                }
              
                Section(header:Text("日期"),content:{
                    
//                    DatePicker(selectedDate.formatted(.dateTime.year().month().day()),selection: $selectedDate,displayedComponents: .date)
                    DatePicker(selection: $selectedDate, displayedComponents: .date) {
                        AnyView(DateView(date: selectedDate))
                    }
                })
            })
            .navigationBarTitle("Settings 設定")
        }
    }
}

struct DateView:View{
    var date: Date
    var body: some View{
        let formatter = DateFormatter()
        formatter.dateFormat = "yyyy-MM-dd"
        return Text(date,formatter:formatter)
    }
}

```
---
### 成果
