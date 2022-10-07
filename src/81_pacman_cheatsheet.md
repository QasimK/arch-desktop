# Pacman usage

*Need a better place than this*

**Browse install packages:**

```sh
pacman -Qq | fzf --preview 'pacman -Qil {}' --layout=reverse --bind 'enter:execute(pacman -Qil {} | less)'
```

(-Qqe for explicitly installed.)

**Mark a package as explicitly installed:**

```sh
pacman -D --asexplicit <pkg>
```

**Find and remove orphan packages:**

```sh
pacman -Qtdq | pacman -Rns -
```

## From `pacman-contrib`

**Search for packages:**

```sh
pacsearch <pkg>
```

**Tree**:

See which packages require `<pkg>`:

```sh
pactree --reverse <pkg>
```
