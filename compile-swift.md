Here’s a **clear, minimal guide** for compiling Swift on **macOS** from the command line — including standalone `.swift` files, multi-file programs, linking frameworks, and creating executables.

---

# ✅ **1. Compile a single Swift file**

If you have:

```
main.swift
```

Compile → run:

```bash
swiftc main.swift -o main
./main
```

---

# ✅ **2. Compile multiple Swift files**

If your project looks like:

```
src/
   main.swift
   midi.swift
   utils.swift
```

Compile them all:

```bash
swiftc src/*.swift -o app
./app
```

Swiftc automatically handles linking between files.

---

# ✅ **3. Compile with a specific SDK (important for macOS frameworks)**

```bash
swiftc -sdk $(xcrun --show-sdk-path) main.swift -o main
```

If you use frameworks like **CoreMIDI**, **CoreAudio**, **AudioToolbox**, or **Metal**, use this.

---

# ✅ **4. Compile Swift with frameworks (Metal, CoreMIDI, etc.)**

Example using **CoreMIDI**:

```bash
swiftc \
   -import-objc-header bridging.h \
   -framework CoreMIDI \
   -sdk $(xcrun --show-sdk-path) \
   main.swift -o midi_app
```

Metal:

```bash
swiftc \
   -framework Metal \
   -framework MetalKit \
   -sdk $(xcrun --show-sdk-path) \
   main.swift shader.swift -o metal_app
```

---

# ✅ **5. Compile with module support (like a small Swift package)**

If you want separate modules:

```
swiftc -emit-module utils.swift -module-name Utils
swiftc main.swift Utils.swiftmodule -o app
```

---

# ✅ **6. Compile Swift with an Objective-C bridging header**

If using Obj-C frameworks or callbacks:

```
swiftc \
  -import-objc-header MyBridge.h \
  -framework CoreAudio \
  -framework CoreMIDI \
  *.swift \
  -o app
```

---

# ✅ **7. Compile & run without producing an executable**

Useful for testing:

```bash
swift main.swift
```

This runs it through the Swift interpreter.

---

# ✅ **8. Build a full project using SwiftPM (recommended)**

```
swift build
swift run
```

Project layout:

```
MyProject/
  Package.swift
  Sources/
     MyProject/
        main.swift
```

This automatically resolves dependencies and builds modules.

---

# ⚙️ Want a Swift compile command for *your* exact project?

Tell me:

- the Swift files involved  
- frameworks you use (CoreMIDI? Metal? CoreAudio? AVFoundation?)  
- any bridging header  
- any custom library or dylib  

I’ll generate the exact `swiftc` command for your project.