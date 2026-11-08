# vim
vim 설치 방법: bash shell에
```
sudo apt install vim
```
입력 후, 암호 입력하면 설치. 인터넷 연결 필요.

vim 실행: vim 파일명

vi 사용 시, vi 실행 후
```
:set nocompatible
:set backspace=indent,eol,start
```
입력.
매 실행 시마다 입력해야 함.


# 1. save-log.sh
```
#!/bin/bash

echo “--- History Save Program ---”
history > commands.txt
echo “Save Complete!”
echo “--- Saved history ---”
cat commands.txt
```

# 2. study-log.sh
```
#!/bin/bash

echo "===== 나의 명령어 기록장 ====="

read -p "저장할 파일명을 입력하세요: " log_file

if [ -z "$log_file" ]; then
    echo "파일명을 입력하지 않았습니다."
elif [ -d "$log_file" ]; then
    echo "같은 이름의 폴더가 있습니다."
else
    save_ok=yes

    if [ -f "$log_file" ]; then
        read -p "이미 있는 파일입니다. 덮어쓸까요? (y/n): " answer

        if [ "$answer" != "y" ]; then
            save_ok=no
        fi
    fi

    if [ "$save_ok" = "yes" ]; then
        history > "$log_file"

        echo "$log_file 파일에 기록을 저장했습니다."
        echo "===== 저장된 기록 ====="

        cat "$log_file"
    else
        echo "저장을 취소했습니다."
    fi
fi
```

# 3. backup.sh
```
#!/bin/bash

echo "===== 자동 파일 백업 프로그램 ====="

read -p "백업할 파일명을 입력하세요: " filename

if [ -f "$filename" ]; then
    mkdir -p backup

    if cp "$filename" backup/; then
        echo "백업이 완료되었습니다."
    else
        echo "백업에 실패했습니다."
    fi
else
    echo "파일이 존재하지 않거나 일반 파일이 아닙니다."
fi
```

## 3-2. backup.sh 실행
```
chmod +x backup.sh
./backup.sh
```
