# PreprocessorVariableArguments

Header files to implement macro argument counting and variable length function and function marco hacks for C/C++
<br>
Uses macro token pasting to tokenize the amount of arguments passed, allowing abstraction with some more dynamic functionality.

<br>

## How it works

Macros passing arguments to add padding before passing the reversed amount of arguments and tokenizing what ends up being the amount of arguments

<br>

### Example

<br>

```

//ex. A macro to write pins as high or low and optionally set to either input or output

#define writeBit(value, bitPosition, bitValue)	((bitValue) ? (value |= (1 << bitPosition)) : (value &= ~(1 << bitPosition)))

#define _WRITE_PINV3(pL, pN, pV) writeBit(__PIN_UTIL_TOKENIZE_REG_NAME(__PIN_UTIL_PREFIX_WRITE_REG, pL), pN, pV)

#define _WRITE_PINV4(pL, pN, pV, pD) writeBit(__PIN_UTIL_TOKENIZE_REG_NAME(__PIN_UTIL_PREFIX_WRITE_REG, pL), pN, pV); writeBit(__PIN_UTIL_TOKENIZE_REG_NAME(__PIN_UTIL_PREFIX_DIR_REG, pL), pN, pD)

#define PIN_WRITE(...) VFUNC(_WRITE_PINV, __VA_ARGS__)


///Macros for helping to build bit masks and values
#define _BUILD_MASK_V1(b0)									(1 << b0)
#define _BUILD_MASK_V2(b0, b1)								(1 << b0 | 1 << b1)
#define _BUILD_MASK_V3(b0, b1, b2)							(1 << b0 | 1 << b1 | 1 << b2)
#define _BUILD_MASK_V4(b0, b1, b2, b3)						(1 << b0 | 1 << b1 | 1 << b2 | 1 << b3)
#define _BUILD_MASK_V5(b0, b1, b2, b3, b4)					(1 << b0 | 1 << b1 | 1 << b2 | 1 << b3 | 1 << b4)
#define _BUILD_MASK_V6(b0, b1, b2, b3, b4, b5)				(1 << b0 | 1 << b1 | 1 << b2 | 1 << b3 | 1 << b4 | 1 << b5)
#define _BUILD_MASK_V7(b0, b1, b2, b3, b4, b5, b6)		   (1 << b0 | 1 << b1 | 1 << b2 | 1 << b3 | 1 << b4 | 1 << b5 | 1 << b6)
#define _BUILD_MASK_V8(b0, b1, b2, b3, b4, b5, b6, b7)			(1 << b0 | 1 << b1 | 1 << b2 | 1 << b3 | 1 << b4 | 1 << b5 | 1 << b6 | 1 << b7)

///Macro for helping to build bit masks and values
#define BUILD_BIT_MASK(...)										VFUNC(_BUILD_MASK_V, __VA_ARGS__)




```

<hr>

Additional links
https://stackoverflow.com/questions/2124339/c-preprocessor-va-args-number-of-arguments,  https://groups.google.com/g/comp.std.c/c/d-6Mj5Lko_s?pli=1
