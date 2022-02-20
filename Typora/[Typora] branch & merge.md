# branch

- 브랜치 만들기

  - git branch {브랜치 이름}

- 브랜치 확인

  - git branch

- 브랜치 지우기

  - git branch -d {브랜치 이름}
  - git branch -D {브랜치 이름}

- 브랜치 이동

  - git switch {브랜치 이름}
  - git checkout {브랜치 이름}
  - 만들면서 이동
    - git switch -c {브랜치 이름}

- 브랜치 merge

  - 기준이 될 브랜치에서!
    - git merge {합칠 브랜치 이름}

  1. 두 브랜치 모두에서 수정사항이 있지만 겹치지 않은 상황
     - 3-way merge
  2. 두 브랜치 모두에서 수정사항이 있고 겹친 상황
     - Conflict 해결 후 commit
  3. 합쳐질 브랜치에만 수정사항이 있는 상황
     - Fast - forword 잘 합쳐짐