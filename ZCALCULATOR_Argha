PARAMETERS : p_inp1 TYPE int2,
             p_inp2 TYPE int2.
DATA: lv_out  TYPE int2,
      lv_sign TYPE c,
      flag    TYPE int1 VALUE 0.
SELECTION-SCREEN :BEGIN OF SCREEN 500 TITLE TEXT-001,  "Where we create a screen with number 500
                  PUSHBUTTON /10(10) add  USER-COMMAND add,
                  PUSHBUTTON 25(10) sub USER-COMMAND sub,
                  PUSHBUTTON 40(10) mul USER-COMMAND multiply,
                  PUSHBUTTON 55(10) div USER-COMMAND divide,
END OF SCREEN 500.
INITIALIZATION. " Where we Initialize the value of our buttons we created above
  add = 'Add'.
  sub = 'Subtract'.
  mul = 'Multiply'.
  div = 'Division'.
AT SELECTION-SCREEN. "Where we do calculation
  CASE sy-ucomm.
    WHEN 'ADD'.
      flag = 1.
      lv_out = p_inp1 + p_inp2.
    WHEN 'SUB'.
      flag = 1.
      lv_out = p_inp1 - p_inp2.
    WHEN 'DIVIDE'.
      IF ( p_inp2 <> 0 ).
        flag = 1.
        lv_out = p_inp1 / p_inp2.
      ELSE.
        flag = 2.
      ENDIF.
    WHEN 'MULTIPLY'.
      flag = 1.
      lv_out = p_inp1 * p_inp2.
  ENDCASE.
START-OF-SELECTION. " Where we show output
  IF p_inp1 IS NOT INITIAL OR p_inp2 IS NOT INITIAL.
    CALL SELECTION-SCREEN '500' STARTING AT 10 10. "Where we call the Screen 500 we created earlier.
    IF flag = 1.
      WRITE: lv_out.
    ELSEIF flag = 2.
      WRITE: 'Cannot Divide a number by 0'.
    ELSEIF flag = 0.
      MESSAGE 'Press any Button to perform any operation!' TYPE 'I'.
    ENDIF.
  ELSE.
    MESSAGE 'Please give both Input to proceed!' TYPE 'I'.
  ENDIF.
