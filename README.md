# Sublime CP (Portable) — Linux

A portable, self-contained Sublime Text setup tailored for competitive programming on Linux. No root, no system install, no messing with your `$HOME`. Unpack, run, code, submit.

> Works entirely in “portable mode”: all settings, packages, and caches live inside this folder (the `Data/` directory). citeturn1search6turn1search8

---

## 📦 What’s inside

```
Sublime_CP_Portable_Linux_Portable/
├─ sublime_text                # The Sublime Text binary (portable)
├─ sublime_text.desktop        # Optional desktop entry for launchers
├─ Data/                       # User data: settings, keymaps, snippets, caches
├─ Packages/                   # Prebundled packages (if any)
├─ IO/                         # Handy I/O files for CP (e.g., input.txt, output.txt)
├─ Icon/                       # App icon(s) for desktop integration
├─ Lib/                        # Support libraries (if provided)
├─ libssl.so.1.1               # Bundled OpenSSL (legacy)  (if present)
├─ libcrypto.so.1.1            # Bundled OpenSSL (legacy)  (if present)
├─ libsqlite3.so               # Bundled SQLite            (if present)
├─ plugin_host-3.3 / -3.8      # Sublime plugin hosts      (if present)
├─ crash_handler               # Sublime crash handler      (if present)
├─ attribution.txt             # Upstream attributions
└─ changelog.txt               # Upstream changelog
```

> The exact file list may vary; see the repo’s file tree for what’s currently checked in. citeturn2view0

---

## 🚀 Quick start (no install)

1. **Download / clone** this folder to any writable location (USB, external drive, or your home directory).  
2. **Make the binary executable (if needed):**
   ```bash
   chmod +x ./sublime_text
   ```
3. **Run it:**
   ```bash
   ./sublime_text
   ```
   That’s it—Sublime will run in **portable mode** because the `Data/` directory is present. citeturn1search6turn1search8

### Optional: add to your desktop launcher
- Copy the desktop file (adjust `Exec=` and `Icon=` paths to your absolute repo path):
  ```bash
  xdg-mime default sublime_text.desktop text/plain
  ```
- Or place `sublime_text.desktop` into `~/.local/share/applications/` and run:
  ```bash
  update-desktop-database ~/.local/share/applications
  ```

> For Linux users, Sublime Text is also offered as archives (which are inherently portable) and via package managers; this repo simply ships a ready-to-run portable bundle. citeturn1search3turn1search10

---

## 🧪 Competitive programming workflow (C++)

This setup includes an `IO/` folder to make local testing easy. Use a build system that compiles the current file and runs it with `IO/input.txt` → `IO/output.txt`.

Create a build system: **Tools → Build System → New Build System…**, paste:

```json
{
  "shell_cmd": "g++ -std=c++17 -O2 -pipe -static-libstdc++ -static-libgcc "$file" -o "$file_path/run" && "$file_path/run" < "${project_path:${folder}}/IO/input.txt" > "${project_path:${folder}}/IO/output.txt"",
  "working_dir": "$file_path",
  "selector": "source.c++, source.cpp, source.cxx",
  "variants": [
    {
      "name": "Run (stdin/stdout)",
      "shell_cmd": "g++ -std=c++17 -O2 -pipe "$file" -o "$file_path/run" && "$file_path/run""
    },
    {
      "name": "Compile Only",
      "shell_cmd": "g++ -std=c++17 -O2 -pipe -Wall -Wextra "$file" -o "$file_path/run""
    }
  ]
}
```

- Save it as `C++17_CP.sublime-build`.
- Select it via **Tools → Build System → C++17_CP**.
- Put your sample tests in `IO/input.txt`, build with **Ctrl+B**. Output lands in `IO/output.txt`.

> Sublime’s build systems let you run external tools and pipe input/output, which is perfect for CP workflows on Linux. citeturn1search7turn1search9

---

## 🧰 Tips & tweaks

- **Compiler:** Switch to `clang++` by replacing `g++` in the build JSON.
- **Multiple files:** For multi-file solutions, swap the compile command to `g++ *.cpp …` or drive it via a simple Makefile and call `make && ./run`.
- **Fast I/O:** Remember to `ios::sync_with_stdio(false); cin.tie(nullptr);`.
- **Snippets & keymaps:** Add your templates in `Data/Packages/User/` (this stays inside the repo—portable).
- **Package Control:** If you add packages, they’ll be stored in `Data/` and travel with this folder (portable).  
- **Themes/UI:** Drop custom themes into `Packages/` or install via Package Control; again, it stays portable.

---

## 🖇️ Desktop integration (manual)

If your launcher doesn’t pick it up, edit `sublime_text.desktop`:

```ini
[Desktop Entry]
Name=Sublime Text (Portable)
Exec=/absolute/path/to/Sublime_CP_Portable_Linux_Portable/sublime_text %F
Icon=/absolute/path/to/Sublime_CP_Portable_Linux_Portable/Icon/sublime-text.png
Type=Application
Categories=Development;TextEditor;
Terminal=false
```

Then place it in `~/.local/share/applications/` and update the database as shown above.

---

## 🔒 Notes on bundled libraries

This bundle may include `libssl.so.1.1`, `libcrypto.so.1.1`, and `libsqlite3.so` to improve portability on distros where these libraries are missing or newer/older than expected. If you experience runtime issues, prefer the system libraries by adjusting `LD_LIBRARY_PATH`, or remove the bundled ones so the system provides them.

---

## 🐞 Troubleshooting

- **Won’t launch / permission denied**  
  Ensure `chmod +x ./sublime_text` and that the folder is on a filesystem that allows exec (not mounted with `noexec`).

- **Blank window on Wayland**  
  Try launching with `QT_QPA_PLATFORM=xcb ./sublime_text` or run inside an X11 session.

- **Build runs but no output**  
  Confirm the path to `IO/input.txt` is correct for your project/folder and that your code reads from `stdin`.

- **Fonts look off**  
  Install preferred monospace fonts (`sudo apt install fonts-firacode` etc.) and select them in **Preferences → Settings**.

---

## 📚 References

- Repo file tree & artifacts (this project). citeturn2view0  
- Sublime Text downloads / Linux info. citeturn1search3  
- Portable mode & installation docs. citeturn1search6turn1search8  
- Example build system patterns for C++ on Linux. citeturn1search7turn1search9

---

## 🔖 License & acknowledgements

This repository bundles upstream Sublime Text artifacts and related attributions as listed in `attribution.txt` and `changelog.txt`. Please ensure you comply with Sublime Text’s license for continued use. citeturn1search3

---

**Happy hacking & speedy submissions!** 🏁
