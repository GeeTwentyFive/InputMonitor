Binds state of `target` input key/click to passed `*OUT_state` address. *Inputs are hooked so state will update even if application is not in focus.*

Target types:
- `INPUTMONITOR__TARGET_KEYBOARD`
- `INPUTMONITOR__TARGET_MOUSE`

Binding:
```c
int InputMonitor__Bind(InputMonitor__target_type targetType, unsigned short target, int *OUT_state)
```

`target` is one of libuiohook's key/click definitions.

^ Ex.: `VC_A`, `MOUSE_BUTTON1`, etc.

Returns 1 upon success, & 0 upon failure.

<br>

All bindings can be cleared via:
```c
InputMonitor__ClearBindings()
```

<br>

Maximum number of possible bindings can be changed by changing the constant: `INPUTMONITOR__MAX_BINDINGS` (default: 256) in `InputMonitor.h`.



# Example:
```c
int stateA = 0;
if (!InputMonitor__Bind(INPUTMONITOR__TARGET_KEYBOARD, VC_A, &stateA)) {
        puts("ERROR: Failed to register 'A'");
        return 1;
}

int stateLMB = 0;
if (!InputMonitor__Bind(INPUTMONITOR__TARGET_MOUSE, MOUSE_BUTTON1, &stateLMB)) {
        puts("ERROR: Failed to register LMB");
        return 1;
}



for(;;) { printf("A: %d\nLMB: %d\n", stateA, stateLMB); Sleep(10); }
```



# Building:
`cc main.c -Lexternal/libuiohook -luiohook`
