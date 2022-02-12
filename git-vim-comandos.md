
# GIT e VIM
## aglomerado rizomático de  comandos úteis


### GIT comandos úteis

Pra configurar login e senha do Github e deixar salvo assim que logar 

```
git config credential.helper store
```
Pra commitar sem alterar o último commit feito. Bom pra quando tu fez o commit e
se deu conta que faltou um detalhe que poderia ter ido com aquele commit.
(dá pra usar o `-m "E uma nova mensagem"` no lugar do `--no-edit`)

```
git commit --amend --no-edit
```


