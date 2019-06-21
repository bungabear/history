# Git 간단 명령어
* ## 다른 브랜치에 push하기  
    git push origin [source]:[dest]  
    * conflict 테스트 해보기

* ## git add 취소하기

        git reset [파일]

* ## git 커밋 합치기, 커밋 메시지 바꾸기

        git rebase -i HEAD~[다룰 커밋 수]

    pick을 해당 명령어로 변경하여 저장
    
        r : 커밋 메세지만 변경
        s : 이전 커밋과 병합

    이후 차례대로 커밋 메세지 입력 혹은 amend, continue 하여 마친뒤,

        # checksum이 변경되어 -f 옵션 필요
        git push -f

* ## git add 취소하기

        git reset [파일]
        

* ## git merge에서 특정 파일 제외하기
    A에 B를 합치는데 일부 파일을 제외.

        git checkout A
        git checkout -b Amerge
        git merge --no-log --no-ff --no-commit B
        git checkout Amerge [머지 안할 파일들]
        git add [머지할 파일들]
        git commit -m "커밋 메세지"
        git push origin Amerge:A 
        git checkout A
        git branch -d Amerge
        git fetch
        git pull
        
