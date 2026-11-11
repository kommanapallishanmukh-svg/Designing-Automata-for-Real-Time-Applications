# Designing-Automata-for-Real-Time-Applications
def validate_email_dfa(email: str) -> bool:
  # States: 0=Start, 1=Local, 2=At, 3=Domain, 4=Dot, 5=TLD_1, 6=Accept
  state = 0
  symbols = {'.', '_', '-'}

  for char in email:
    if state == 0:
      if char.isalnum():
        state = 1
      else:
        return False
    elif state == 1:
      if char.isalnum() or char in symbols:
        state = 1
      elif char == '@':
        state = 2
      else:
        return False
    elif state == 2:
      if char.isalnum():
        state = 3
      else:
        return False
    elif state == 3:
      if char.isalnum() or char == '-':
        state = 3
      elif char == '.':
        state = 4
      else:
        return False
    elif state == 4:
      if char.isalnum():
        state = 5
      else:
        return False
    elif state == 5:
      if char.isalnum():
        state = 6
      else:
        return False
    elif state == 6:
      if char.isalnum():
        state = 6
      elif char == '.':
        state = 4
      else:
        return False

  return state == 6
