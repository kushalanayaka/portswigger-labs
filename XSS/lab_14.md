# 🔐 Lab 14: Reflected XSS into HTML Context with Most Tags and Attributes Blocked

## 🧩 Objective
To exploit a vulnerability by bypassing filters that block most HTML tags and attributes

## 🔍 Vulnerability
The application attempts to block common XSS paloads by filtering HTML tags and attributes,
but fails to properly sanitaize all the possible vectors, allowing execution of javascript.

## ⚙️ Payload Used
`<body onresize='print()>`

## 🔎 Context
- **Source:** User input (search parameter)  
- **Sink:** HTML rendering  
- **Type:** Reflected XSS with filter bypass  

## 🔎 Analysis
1. The application blocks common tags like `<script>`  
2. Most attributes are also filtered  
3. Some tags like `<body>` are still allowed  
4. Used Burp suite Intruder to check tag.  
5. JavaScript executes automatically when the Body loads 

## 💡 Payload Explanation
- `<body>` → allowed HTML tag in many filters  
- `onresize` → event triggered when body loads  
- `print()` → JavaScript execution  

👉 Why this payload:
- Bypasses tag-based filters  
- Uses less common but valid HTML elements  
- Executes automatically without user interaction  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Enter the following payload:  
   `<body onresize='print()'>`
3. Submit the input  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming successful filter bypass and XSS.

## 🧠 Key Learning
Blocking common tags is not sufficient. Attackers can use alternative HTML elements and event handlers to bypass filters.

## 🛡️ Prevention
- Use context-aware output encoding  
- Avoid blacklist-based filtering  
- Implement strict input validation  
- Use Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1349" height="659" alt="LAB14_5" src="https://github.com/user-attachments/assets/66937479-4905-4a7f-b94a-97a0cf79744c" />

**Figure 1: Injecting Body payload into input field**

<br>

<img width="1357" height="692" alt="LAB14_1" src="https://github.com/user-attachments/assets/6f09d15f-5844-45b4-9d9f-56cd4ca21586" />

**Figure 2: Setting up Burp Suite intruder to check the tag using some builtin tags**

<br>

<img width="1325" height="668" alt="LAB14_2" src="https://github.com/user-attachments/assets/d6964523-bf42-44d9-9005-e861bbb71409" />

**Figure 3: onresize tag with 200 OK response is selected**

<br>
<img width="1357" height="693" alt="LAB14_3" src="https://github.com/user-attachments/assets/69eaead3-6ac7-427f-bf73-63f4719e37cd" />

**Figure 4: After the resizing manualy print() working**

<br>
<img width="1331" height="676" alt="LAB14_4" src="https://github.com/user-attachments/assets/fec1b3c3-400e-417c-9f84-f05953110b24" />

**Figure 5: For the automatic load used exploit sever and send it to JavaScript execution via onload event (Lab Solved)**
