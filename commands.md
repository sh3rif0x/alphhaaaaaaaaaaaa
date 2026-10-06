git clone https://github.com/sh3rif0x/solid-law-website.git
cd solid-law-website
find . -type f \( -name "home.js" -o -name "script.js" -o -name "home.css" \)

┌──(boot㉿radar)-[~/Desktop/cutlab-friseursalon]
└─$ { find . -type f -name '*.html' -print -exec sh -c 'printf "\n===== %s =====\n" "$1"; cat "$1"' _ {} \; ; find ./js -type f -name '*.js' -print -exec sh -c 'printf "\n===== %s =====\n" "$1"; cat "$1"' _ {} \; ; } > x.txt && xclip -selection clipboard < x.txt && rm x.txt

source /home/boot/Desktop/el_makhzan/mid/x/cv/venv/bin/activate && python -m pip install "rembg[cpu]" && rembg i ~/Desktop/hbhb.png ~/Desktop/output.png