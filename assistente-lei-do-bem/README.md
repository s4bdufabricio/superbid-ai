
Comando para gerar o log de commits

```
git log --since="2021-01-01" --pretty=format:"%h,%an,%ad,%s" --date=format:"%Y-%m" > commits-terminal.log
```