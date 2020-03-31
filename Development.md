원격 서버를 경유하여 연구 개발을 진행하는 경우 다음과 같은 절차를 따른다.

1. 원격 서버 접속
- 분석 코드가 직접 수행될 서버를 접속한다.
```bash
ssh -p 300xx 651xxx@10.12.xx.xx
```

2. Git configuration
- Git 사용을 위한 기본 Git 설정을 수행
```bash
git config --global user.email "minhoe.hur@hyundai.com"
git config --global user.name "minhoe"
```

3. Github repository clone
- 모든 소스 코드는 Github에 저장하고, 분석 시 서버로 가져와서 진행을 한다.
- 분석이 완료되면 서버 내 파일은 삭제하여도 무방하다.
```bash
cd your_project_home_folder_to_be_used
git clone https://github.com/hkmc-airlab/SF_WheelAlignment.git
```

4. Local branch 생성
- Master Branch에 합병하기 전 안전성을 위해 우선 임시의 Branch를 생성한다.
```bash
# Git local branch 생성
git checkout -b new_model
```

5. Do Research!
```bash
# Some files may be added..
```

6. (Optional)Gitignore update
- 분석 업무를 진행하다 얻은 중간 결과파일이나 결과 이미지들은 용량이 커서 github에 동기화하기 어렵다.
- 이러한 파일들이 저장된 경로를 github push에서 제외되도록 설정한다.
```bashrc
cd your_project_home_folder_to_be_used/SF_WheelAlignment
vim .gitignore
```

7. 변경 사항을 local branch에 반영
- 이 경우 new_model branch에 적용된다.
```bash
git add .
```

8. 변경 사항을 local branch에 commit
- commit message를 입력한다.
```bashrc
git commit -m 'Add first commit'
```

9. 변경 사항을 remote branch에 push
```bash
git push origin new_model
```

10. 변경 사항을 local master branch에 반영
- 현재 local master branch에는 반영이 되어 있지 않다. 방금 반영한 신규 branch를 master로 반영하기 위해서는 다음의 방안이 있다.

#### Case 1. remote new_model branch를 local master branch로 반영

11. master branch로 이동
```bash
git checkout master
```

12. remote new_model branch를 pull
- 아래 과정을 통해 new_model 내용이 local origin(master)으로 반영된다.
```bash
git pull origin new_model
```

13. local branch 삭제
- 새로운 적용 이후 기능을 다 한 branch는 삭제해도 무방하다.
```bash
git branch -D new_model
```

14.remote에서 new_model branch와 master 내용 검토 후 merge를 진행한다. 
- 이후 필요 시 신규 branch를 삭제하여 마무리한다.

#### Case 2. remote에서 branch merge 이후 remote master branch를 local master branch로 반영




