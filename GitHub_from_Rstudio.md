# Pequeña guía de uso de GitHub desde RStudio

Referencia: [Happy Git and GitHub for the useR](https://happygitwithr.com/)

# 1. Preparativos

Todos estos pasos sólo se han de hacer una vez

-   Instalar Git, Instalar Git Client, en mi caso ya tenía instalado GItHub Desktop.
-   Instalar RStudio: Primero instalar R, luego Rtools y finalmente RStudio.
-   Crear una cuenta en GitHub

## Preséntate a Git

Se trata de decirle a Git quien es el cliente. Hay dos opciones,una manual en la terminal y otra a través de un paquete de R

Pasos en la terminal.(R Studio tiene incrustada una terminal del estilo de Bash)

```{bash}
git config --global user.name "Jane Doe"
git config --global user.email "jane@example.com"
git config --global --list
```

Sustituir el usuario y el **email por los que se usaron en el registro de GitHub**

O bien re puede usar el paquete "use this" de R para hacer este proceso. En este caso primero se necesita tener instalado el paquete. En la consola(no la terminal):

```{r}
## install if needed (do this exactly once):
## install.packages("usethis")

library(usethis)
use_git_config(user.name = "Jane Doe", user.email = "jane@example.org")
```

Sustituir el por el nombre de usuario e email.

## Configure the default name for an initial branch

You can set your default initial branch name to main like so, in the shell:

```{bash}
git config --global init.defaultBranch main
```

or from R (the default for name is "main"):

```{r}
usethis::git_default_branch_configure()
```

## 3. Credenciales

Para trabajar con GitHub se utiliza no el email y el password de la cuenta, sino un

## Personal access token for HTTPS

Go to <https://github.com/settings/tokens> and click “Generate token”.

Or, from R, do:

```{r}
usethis::create_github_token()
```

**Store the PAT explicitly right now**

**El PAT caduca por lo que será necesario renovarlo**

In R, call `gitcreds::gitcreds_set()` to get a prompt where you can paste your PAT

## Confirm that you can push to / pull from GitHub from the command line

### 1. Make a repo on GitHub

Go to <https://github.com> and make sure you are logged in.

Near “Repositories”, click the big green “New” button. Or, if you are on your own profile page, click on “Repositories”, then click the big green “New” button.

How to fill this in:

-   Repository template: No template.
-   Repository name: myrepo or whatever you wish (we’ll delete this soon).
-   Description: “Repository for testing my Git/GitHub setup” or similar. It’s nice to have something here, so you’ll see it appear in the README.
-   Public.
-   Initialize this repository with: Add a README file.
-   Click the big green button that says “Create repository”

Now click the big green button that says “\<\> Code”.

Copy a clone **HTTPS** URL to your clipboard

### 2.Clone the repo to your local computer

Move to te working directory

In terminal:

```{bash}
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```

Change url to the actual one

### 3.Make a local change, commit, and push

Add a line to README and verify that Git notices the change. In Terminal:

```{bash}
echo "A line I wrote on my local computer  " >> README.md
git status
```

Track the changes of the modified file Save file(s) and commit.

```{bash}
git add README.md
git commit -m "A commit from my local computer"
git push
```

### 4.Confirm the local change propagated to the GitHub remote

Go back to the browser. I assume we’re still viewing your new GitHub repo, and Refresh (F5).

### 5.Clean it up

If you’re ready to conclude this test of your Git installation and GitHub configuration, we can clean up the test repository now

1.  In **local** delete the directory
2.  In **GitHub in the browser**, go to your repo’s landing page on GitHub. Click on “Settings”.Scroll down, click on “delete repository,” and do as it asks.

# 2. Connect RStudio to Git and GitHub

