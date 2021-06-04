# Hello World!

## Yet Another Self Promoting Blog

Denna blog är ett pompöst och oironiskt sätt att visa närvaro på nätet. Har för avsikt att även använda detta som en saniterad form av egna anteckningar kring teknologier jag använder eller undersöker.

### Rubrik 3

Nedan följer ett kodblock

    #!/usr/bin/env bash
    printf "Hello World!\n"

Även detta är ett kodblock

```bash
#!/usr/bin/env bash

printf "[          ]\r["
for i in {0..9}; do
    printf "#"
    sleep 0.5
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
