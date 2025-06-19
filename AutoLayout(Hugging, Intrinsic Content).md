✅ What is Auto Layout in iOS?
- Auto Layout is a powerful constraint-based layout system used in iOS (and macOS) to create responsive and adaptive user interfaces.
Rather than manually setting frames (x, y, width, height), you define rules (constraints) that describe how views relate to each other.

### 🔧 How Auto Layout Works
**Auto Layout:**
Takes your constraints (rules).
Uses a system called the Cassowary algorithm to solve them.
Determines the size and position of every view.

### ⚙️ Key Concepts in Auto Layout

| Term                       | Meaning                                                                              |
| -------------------------- | ------------------------------------------------------------------------------------ |
| **Constraint**             | A rule defining how one view relates to another (e.g., leading, trailing, width).    |
| **Anchor**                 | An edge or dimension of a view (e.g., `topAnchor`, `heightAnchor`).                  |
| **Intrinsic Content Size** | The natural size of a view based on its content (e.g., a label grows based on text). |
| **Hugging Priority**       | Resistance to growing larger than its content.                                       |
| **Compression Resistance** | Resistance to shrinking smaller than its content.                                    |
| **Ambiguous Layout**       | When constraints are not enough to determine one layout.                             |

🧠 What is “Content” in Auto Layout?
In this context:
Content refers to the inner data of a view (like text in a label or image in an UIImageView).
Auto Layout can size views based on their content using intrinsic content size.

Example:

let label = UILabel()
label.text = "Hello"
label.translatesAutoresizingMaskIntoConstraints = false

The label’s intrinsic content size will be the size required to show "Hello".
If no width/height constraints are added, it will size itself automatically.

### 🧭 Why Use Auto Layout?

| Benefit        | Description                                                 |
| -------------- | ----------------------------------------------------------- |
| ✅ Responsive   | Works across all screen sizes and orientations.             |
| ✅ Dynamic      | Supports rotation, resizing, multi-language, accessibility. |
| ✅ Maintainable | Easier to manage than hardcoding frames.                    |

✅ Meaning of Specific Values: 249, 250, 251, 252
These values are relative — Auto Layout always compares priorities between views.

| Priority | Description                                                                            |
| -------- | -------------------------------------------------------------------------------------- |
| **249**  | Slightly **weaker** than default. More willing to grow/stretch or compress.            |
| **250**  | **Default** system priority for content hugging (i.e., neutral baseline).              |
| **251**  | Slightly **stronger** than default. More resistant to stretching.                      |
| **252**  | Even **stronger** than 251. This view will prefer to hug its content more than others. |


### 🧰 SwiftUI Equivalent?
In SwiftUI, Auto Layout is replaced with declarative layout using containers like VStack, HStack, ZStack, and modifiers like .frame(), .padding(), etc. But under the hood, SwiftUI still respects layout rules similar to Auto Layout.

### 📌 Summary
| Term                       | Meaning                                              |
| -------------------------- | ---------------------------------------------------- |
| **Auto Layout**            | Constraint-based layout system to build adaptive UIs |
| **Constraint**             | Rule that defines layout relationships               |
| **Intrinsic Content Size** | Natural size of a view based on its content          |
| **Hugging/Compression**    | Priority settings for how views grow/shrink          |



