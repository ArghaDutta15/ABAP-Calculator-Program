# ABAP Calculator Program

A simple yet functional calculator application developed in **ABAP**, capable of performing basic arithmetic operations such as **addition, subtraction, multiplication, and division** directly within the SAP environment.  

This project demonstrates how to build interactive programs in ABAP using **selection screens**, **pushbuttons**, and **event handling** with `sy-ucomm`.

---

## 🚀 Features
- **User-friendly interface** with pushbuttons for operations.
- Supports:
  - Addition
  - Subtraction
  - Multiplication
  - Division (with zero-division handling)
- **Input validation** for missing inputs and division by zero.
- Clear output display using the `WRITE` statement.

---

## 📂 Project Structure
/ABAP-Calculator
├── calculator_program.abap # Main ABAP source code
├── README.md # Project documentation


---

## 🖥️ How It Works
1. User enters two numbers as input.
2. Clicks on one of the four operation buttons.
3. The program:
   - Executes the corresponding arithmetic operation.
   - Displays the result on the screen.
   - Shows a message if inputs are missing or division by zero is attempted.

---

## 💻 Code Example
```abap
PARAMETERS: p_inp1 TYPE i,
            p_inp2 TYPE i.

DATA: lv_out  TYPE i,
      flag    TYPE i VALUE 0.

SELECTION-SCREEN: BEGIN OF SCREEN 500 TITLE TEXT-001,
                  PUSHBUTTON /10(10) add  USER-COMMAND add,
                  PUSHBUTTON 25(10) sub  USER-COMMAND sub,
                  PUSHBUTTON 40(10) mul  USER-COMMAND multiply,
                  PUSHBUTTON 55(10) div  USER-COMMAND divide,
                  END OF SCREEN 500.

INITIALIZATION.
  add = 'Add'. sub = 'Subtract'.
  mul = 'Multiply'. div = 'Division'.

AT SELECTION-SCREEN.
  CASE sy-ucomm.
    WHEN 'ADD'.      flag = 1. lv_out = p_inp1 + p_inp2.
    WHEN 'SUB'.      flag = 1. lv_out = p_inp1 - p_inp2.
    WHEN 'DIVIDE'.   IF p_inp2 <> 0. flag = 1. lv_out = p_inp1 / p_inp2. ELSE. flag = 2. ENDIF.
    WHEN 'MULTIPLY'. flag = 1. lv_out = p_inp1 * p_inp2.
  ENDCASE.

START-OF-SELECTION.
  IF p_inp1 IS NOT INITIAL AND p_inp2 IS NOT INITIAL.
    CALL SELECTION-SCREEN '500' STARTING AT 10 10.
    IF flag = 1. WRITE: / 'Result:', lv_out.
    ELSEIF flag = 2. WRITE: / 'Cannot divide a number by zero.'.
    ELSE. MESSAGE 'Press any button to perform an operation!' TYPE 'I'.
    ENDIF.
  ELSE.
    MESSAGE 'Please provide both inputs to proceed!' TYPE 'I'.
  ENDIF.

##🛠️ Tech Stack
Language: ABAP

Platform: SAP NetWeaver (via SAP Logon)

Editor: ABAP Editor (SE38)
