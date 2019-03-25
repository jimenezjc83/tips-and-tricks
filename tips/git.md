Checkout remote git branch:
---------------------------

* git fetch origin
* git branch -v -a
* git checkout -b test origin/test

Ver el history de un archivo:
-----------------------------

* git log --follow -p filename

Comparar los cambios locales con los cambios remotos:
-----------------------------------------------------

* git diff [filename]

Esconder los cambios locales y regresar al último pull:
(http://git-scm.com/book/en/Git-Tools-Stashing)
-------------------------------------------------------

* git stash
* git stash list
* git stash apply
* git stash pop
* git stash drop stash@{0}

Renombrar un branch local y remotamente:
----------------------------------------

* git branch -m new_branch         	    # Rename branch locally, you should be stand in the branch that you want to rename    
* git push origin :old_branch                 # Delete the old branch    
* git push --set-upstream origin new_branch   # Push the new branch, set local branch to track the new remote

Gestion de commits
-------------------------
* git revert commit_id			# Revertir un commit remoto
* git reset --hard HEAD~1			# Revertir el último commit local sin guardar los cambios
* git reset --soft HEAD~1			# Revertir el último commit local guardar los cambios

Remover branches locales que ya no existan remotamente
------------------------------------------------------

**Linux:**
```sh
* git fetch -p && for branch in `git branch -vv | grep ': gone]' | gawk '{print $1}'`; do git branch -D $branch; done
```

**Mac:**
```sh
* git fetch -p && for branch in `git branch -vv | grep ': gone]' | awk '{print $1}'`; do git branch -D $branch; done
```

Cambiar el autor del ultimo commit
----------------------------------
* git commit --amend --reset-author

Crear Tags
----------
* git tag -a build106.5 -m "Descripcion del tag"
* git push origin build106.5

Eliminar tags remotos
---------------------
* git tag -d 12345
* git push origin :refs/tags/12345
* git push --delete origin v1.11.12-SNAPSHOT  (Alternativo)

Lista de branch recientemente modificados
-----------------------------------------
```sh
* for branch in `git branch -r | grep -v HEAD`;do echo -e `git show --format="%ci %cr" $branch | head -n 1` \\t$branch; done | sort -r
```

Limpiar workspace incluyendo cambios y archivos/directorios creados
-------------------------------------------------------------------
* git clean -f -d
* git clean -xfd (Limpia archivos dentro del .gitignore, agregar n para hacer un dry run)
