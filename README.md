import os, zipfile, shutil

repo = "/mnt/data/happy-birthday-diki-github-v2"
if os.path.exists(repo):
    shutil.rmtree(repo)
os.makedirs(repo)

code = r'''import threading
import time
import os
import shutil

cake = r"""
           _..._  ,s$$$s.
         .$$$$$$$s$$ss$$$$,
         $$$sss$$$$s$$$$$$$
         $$ss$$$$$$$$$$$$$$
         '$$$s$$$$$$$$$$$$'
          '$$$$$$$$$$$$$$'
            S$$$$$$$$$$$'
             '$$$$$$$$$'
               '$$$$$'
                '$$$'
                  ;
                 ;
"""

# Large block font, deliberately matching the giant multi-line
# ASCII-letter style of the original "wish" section.
FONT = {
"A":["   /$$   ","  /$$$$  "," /$$  $$ ","/$$$$$$$$","| $$  | $$","| $$  | $$","| $$  | $$"],
"D":["$$$$$$  ","$$   $$ ","$$    $$","$$    $$","$$    $$","$$   $$ ","$$$$$$  "],
"E":["$$$$$$$$","$$      ","$$      ","$$$$$$  ","$$      ","$$      ","$$$$$$$$"],
"H":["$$    $$","$$    $$","$$    $$","$$$$$$$$","$$    $$","$$    $$","$$    $$"],
"I":["$$$$$$$$","   $$   ","   $$   ","   $$   ","   $$   ","   $$   ","$$$$$$$$"],
"K":["$$   $$ ","$$  $$  ","$$ $$   ","$$$$    ","$$ $$   ","$$  $$  ","$$   $$ "],
"N":["$$   $$ ","$$$  $$ ","$$$$ $$ ","$$ $$$$ ","$$  $$$$","$$   $$$","$$    $$"],
"R":["$$$$$$$ ","$$    $$","$$    $$","$$$$$$$ ","$$  $$  ","$$   $$ ","$$    $$"],
"S":[" $$$$$$$","$$     "," $$     ","  $$$$$ ","      $$","      $$","$$$$$$$ "],
"U":["$$    $$","$$    $$","$$    $$","$$    $$","$$    $$","$$    $$"," $$$$$$$"],
" ":["        "]*7,
}

def clear():
    os.system("cls" if os.name == "nt" else "clear")

def center(s):
    return s.center(shutil.get_terminal_size((110,30)).columns)

def render(name, visible):
    rows=[]
    for r in range(7):
        parts=[]
        for i,ch in enumerate(name):
            parts.append(FONT.get(ch,FONT[" "])[r] if i < visible else "        ")
        rows.append("  ".join(parts).rstrip())
    return rows

def type_text(text, delay=0.01):
    for ch in text:
        print(ch, end="", flush=True)
        time.sleep(delay)

def animate_name(name):
    # Each character appears separately, just like the requested
    # letter-by-letter effect, while retaining the large original style.
    for visible in range(1, len(name)+1):
        clear()
        print("\n")
        for row in render(name, visible):
            print(center(row))
        print()
        time.sleep(0.28)

def task1():
    clear()
    type_text(cake, 0.002)
    time.sleep(0.6)

    clear()
    print(center("HAPPY BIRTHDAY TUMI"))
    print()
    time.sleep(0.8)

    # Same large ASCII treatment as the original "LOUIS" lettering,
    # changed to DIKI SUHENDRA.
    animate_name("DIKI SUHENDRA")

    time.sleep(0.6)
    print()
    print(center("Thank you God for the long life you have given me."))
    print()

t1 = threading.Thread(target=task1, name="t1")
t1.start()
t1.join()
'''

with open(os.path.join(repo, "happy_birthday_diki.py"), "w", encoding="utf-8") as f:
    f.write(code)

with open(os.path.join(repo, "README.md"), "w", encoding="utf-8") as f:
    f.write("""# Happy Birthday Tumi — Diki Suhendra

Python terminal animation based on the original ASCII birthday script.

- Large multi-line ASCII lettering
- `DIKI SUHENDRA` replaces the original name
- Characters appear one by one
- No external packages required

Run:

```bash
python happy_birthday_diki.py
