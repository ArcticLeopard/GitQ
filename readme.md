# GitQ – Git Quick Alias Toolkit 🚀

**GitQ** is a collection of powerful Git aliases that automate common workflows like squashing commits, safely pushing, and managing stash – ideal for solo developers who want to keep a clean Git history with zero hassle.

## 🔧 Installation

Paste the following into your terminal:


# Alias: git re – auto-squash last commit (no push)
```bash
git config --global alias.re '!f() { \
  git stash --keep-index && \
  last_msg=$(git log -1 --pretty=%B) && \
  git reset --soft HEAD~1 && \
  git commit -am "$last_msg" && \
  git stash pop; \
}; f'
```
# Alias: git rep – same as `re` but with force-push

```bash
git config --global alias.rep '!f() { \
  git stash --keep-index && \
  last_msg=$(git log -1 --pretty=%B) && \
  git reset --soft HEAD~1 && \
  git commit -am "$last_msg" && \
  git push --force-with-lease && \
  git stash pop; \
}; f'
```

# Alias: git rew – automatic squash/reset without push
```bash
git config --global alias.re '!f() { \
  git stash --keep-index && \
  git commit -am "Update" && \
  old_commit=$(git rev-parse HEAD~1) && \
  GIT_COMMITTER_DATE="$(git show -s --format=%cI $old_commit)" \
  git reset --soft $old_commit && \
  git commit -C $old_commit && \
  git stash pop; \
}; f'
```
# Alias: git rewp – same as `rew` but with force-push

```bash
git config --global alias.rep '!f() { \
  git stash --keep-index && \
  git commit -am "Update" && \
  old_commit=$(git rev-parse HEAD~1) && \
  GIT_COMMITTER_DATE="$(git show -s --format=%cI $old_commit)" \
  git reset --soft $old_commit && \
  git commit -C $old_commit && \
  git push --force-with-lease && \
  git stash pop; \
}; f'
```