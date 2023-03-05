# SwiftUI_chipsView_withlabel

```swift
struct ContentView: View {
    
    let words = ["Action movies are good", "Horror one", "Comedy is good", "Adventure Park", "Kids", "Sillicon Valley"]
    
    var body: some View {
        TagsView(items: self.words)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

struct TagsView: View {
    
    let items: [String]
    var grouptedItems: [[String]] = [[String]]()
    let screenWidth: CGFloat = UIScreen.main.bounds.width
    
    init(items: [String]) {
        self.items = items
        self.grouptedItems = self.createGroupedItems(items)
    }
    
    var body: some View {
        VStack(alignment: .leading) {
            ForEach(self.grouptedItems, id: \.self) { subItems in
                HStack {
                    ForEach(subItems, id: \.self) { word in
                        Text(word)
                            .padding()
                            .background(Color.blue)
                            .foregroundColor(.white)
                            .clipShape(RoundedRectangle(cornerRadius: 10, style: .continuous))
                    } //: FOREACH
                } //: HSTACK
            } //: FOREACH
            
            Spacer()
        } //: VSTACK
    }
    
    private func createGroupedItems(_ items: [String]) -> [[String]] {
        var grouptedItems: [[String]] = [[String]]()
        var tempItems: [String] = [String]()
        var width: CGFloat = 0
        for word in items {
            let label = UILabel()
            label.text = word
            label.sizeToFit()
            let labelWidth = label.frame.size.width + 32
            if width + labelWidth + 32 < self.screenWidth {
                width += labelWidth
                tempItems.append(word)
            } else {
                width = labelWidth
                grouptedItems.append(tempItems)
                tempItems.removeAll()
                tempItems.append(word)
            }
        }
        grouptedItems.append(tempItems)
        return grouptedItems
    }
    
}

```
