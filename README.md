# Nim cheatsheet

### Type parsing
```nim
from strutils import parseInt

let n = parseInt(readLine(stdin))
```

### Generators
```nim
const fac4 = (var x = 1; for i in 1..4: x *= i; x)
```

### Procedures
```nim
proc sumTillNegative(x: varargs[int]): int =
  for i in x:
    if i < 0:
      return
    result = result + i
    
echo sumTillNegative(3, 4 , -1 , 6)
```

### Nested if
```nim
proc printSeq(s: seq, nprinted: int = -1) =
  var nprinted = if nprinted == -1: s.len else: min(nprinted, s.len)
  for i in 0 .. <nprinted:
    echo s[i]
```

### Procedure without result
```nim
discard yes("Can I ask a useless question?")
```
OR
```nim
proc p(x, y: int): int {.discardable.} =
  return x + y

p(3, 4)
```

### Operator overload
```nim
proc `$` (x: myDataType): string = ...
```

### Preliminary declaration 
```nim
proc even(n: int): bool

proc odd(n: int): bool =
  assert(n >= 0) 
  if n == 0: false
  else:
  n == 1 or even(n-1)

proc even(n: int): bool =
  assert(n >= 0) 
  if n == 1: false
  else:
  n == 0 or odd(n-1)
```

### Yielding iterator
```nim
iterator countup(a, b: int): int =
  var res = a
  while res <= b:
    yield res
    inc(res)
```

### Internal representation of types ($ vs repr)
```nim
var
  myBool = true
  myCharacter = 'n'
  myString = "nim"
  myInteger = 42
  myFloat = 3.14
echo($myBool, ":", repr(myBool))
# --> true:true
echo($myCharacter, ":", repr(myCharacter))
# --> n:'n'
echo($myString, ":", repr(myString))
# --> nim:0x10fa8c050"nim"
echo($myInteger, ":", repr(myInteger))
# --> 42:42
echo($myFloat, ":", repr(myFloat))
# --> 3.1400000000000001e+00:3.1400000000000001e+00
```
