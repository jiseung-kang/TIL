tabindex : -1 ν¬ν¨ μ¬λΆ

# focusable

<aside>
π‘ λνν μμμλ tabindex=β0βμ μΆκ°ν΄ ν¬μ»€μ€ κ°λ₯νκ² λ§λ€μ΄μΌ νλ€.

</aside>

- μμμ focus νλ λ°©λ²
  - element.focus()
  - tabindex=0

## tabindex=β0β

- κ°μ΄ 0μ΄λ©΄ μμκ° HTML λ¬Έμμ μμ μμλ₯Ό κΈ°λ°μΌλ‘ νλ κΈ°λ³Έ ν¬μ»€μ€ μμμ μΌλΆμμ λνλΈλ€.
- μμ κ°μ μ¬μ©νλ©΄ κΈ°λ³Έ μμμ μμλ³΄λ€ λ¨Όμ  λ°°μΉλλ―λ‘ λΌλ¦¬μ μΌλ‘ νΌλμ€λ½λ€.

## tabindex=β-1β

- μμ°¨μ  ν€λ³΄λ νμμΌλ‘ μμμ λλ¬ν  μ μλ€.
- JavaScript, λ§μ°μ€ ν΄λ¦­μΌλ‘ μ΄μ μ λ§μΆ μ μλ€.

# Tabbable

- μ ννμ§ μμ μμ
  - hidden
  - aria-selected=βfalseβ
  - tabindex=β-1-
- μ νν μμ
  - hidden μ κ±°
  - aria-selected=βtrueβ
  - tabindex=β0β
