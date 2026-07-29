# Git

```
git remote -v
```

```
git remote rm origin
```

```
git remote add origin <url>
```

```
git branch -M main
```

```
git push -u origin main
```

```
git config --global user.name <username>
```

```
git config --global user.email <username>
```
How to git your local folder
1. Create a new repo (without README.md)

2. Go to your folder and open the terminal
   
3. Paste the code under "…or create a new repository on the command line" on your terminal.
  Example:
  ```
  echo "# SAV" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main
  git remote add origin https://github.com/Athenachc/SAV.git
  git push -u origin main
  ```
