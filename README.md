# LocalizableToExcel
/*
Make easy to change Localizable.strings to spread sheet.

How To Use
1. Clone or download
2. Download ZIP
3. Open README.md file
4. Copy & Paste below code to Playground.
5. Copy & Paste your Localizable.strings file string to localizableString.
*/

var localizableString = """
    // insert your Localizable.strings file string here!!!
"""

enum Status {
    case stop
    case startKey
    case readyValue
    case startValue
}

var status: Status = .stop

var key = String()
var value = String()
var char: Character!
var keyList = [String]()
var valueList = [String]()
while !localizableString.isEmpty {
    char = localizableString.removeFirst()
    if char == "\"" {
        switch status {
        case .stop:
            status = .startKey
        case .startKey:
            status = .readyValue
        case .readyValue:
            status = .startValue
        case .startValue:
            status = .stop
            keyList.append(key)
            valueList.append(value)
            key = ""
            value = ""
        }
    } else {
        switch status {
        case .stop:
            _ = "pass"
        case .startKey:
            key.append(char)
        case .readyValue:
            _ = "pass"
        case .startValue:
            if char == "\n" {
                value.append("\\n")
            } else {
                value.append(char)
            }
        }
    }
}

print("[Key Started]\n")
for item in keyList {
    print(item)
}
print("\n[Key Ended & Value Started]\n")
for item in valueList {
    print(item)
}
print("\n[Value Ended]")
