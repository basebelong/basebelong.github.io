# Hello World!

## Yet Another Self Promoting Blog

Denna blog är ett pompöst och oironiskt sätt att visa närvaro på nätet. Har för avsikt att även använda detta som en saniterad form av egna anteckningar kring teknologier jag använder eller undersöker.

### Kodsnippets

Ignorera. Testar bara hur kod ser ut.

    #!/usr/bin/env bash
    printf "Hello World!\n"

En phony progress bar. Högerjusterar. Tar text till vänsterspalten som argument.

```bash
#!/usr/bin/env bash

width=$(tput cols)
padding=$(( width - 20 ))
message="$*"

printf "%s" "$message"
printf "\r\033[${padding}C[          ]\r\033[${padding}C["
for i in {0..9}; do
    printf "#"
    sleep 0.3
done
printf "] Done.\n"
```

### Sitekarta

Poster. I datumordning. Försöker att hålla rubriken rimlig för att underlätta sökande på sidan efter intresseområde. Att 'Ctrl + F' (eller '/' om man kör något vim-plugin till sin webläsare) och skriva t.ex. 'LXD' *skall* visa relevanta artiklar.

<ul>
    {% for post in site.posts %}
        <li>
            <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
