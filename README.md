# dry
Sometimes I find myself googling more than once to find a solution for some problems I've encountered before. From now on, I'll be using this repository to record this kind of stuff.

## Bash Scripting

How can I get the absolute path of the current script?
```shell
# Use VAR=`get_absolute_path` to get the returned value
get_absolute_path() {
    SOURCE="${BASH_SOURCE[0]}"

    # Resolve $SOURCE until the file is no longer a symlink.
    while [ -h "$SOURCE" ]; do
        DIR="$( cd -P "$( dirname "$SOURCE" )" && pwd )"
        SOURCE="$(readlink "$SOURCE")"

        # If $SOURCE was a relative symlink, we need to resolve it
        # relative to the path where the symlink file was located.
        [[ $SOURCE != /* ]] && SOURCE="$DIR/$SOURCE"
    done
    DIR="$( cd -P "$( dirname "$SOURCE" )" && pwd )"

    echo "${DIR}"
}
```

How can I redirect `stdout` and `stderr` to a file?
```shell
$command > $redirectedFilePath 2>&1 
```

How can I get the PID (process ID) of a process I run in detached mode?
```shell
python example.py &
PID_OF_COMMAND=$!
```

How can I wait for the user confirm whether he/she wants the script to continue executing or not?
```shell
confirm_to_continue() {
    message=$1

    while true; do
        read -p "${message}" answer

        case $answer in
            [yY]* ) break;;

            [nN]* ) echo "Quiting"
                    exit;;

            * ) echo "Enter y or n, please.";;
        esac
    done
}
```

How can I get a list of the largest top 10 files and directories under the current directory?
```shell
du -hsx * | sort -rh | head -10
```

How can I generate a random number between 1 and 10?
```shell
NUM=$(( ( RANDOM % 10 ) + 1 ))
```

How can I get the length of an array defined in bash?
```shell
my_array=(1 2 3)
length_of_array=${#my_array[@]}
```

How can I get the number of cores (in MacOSX)?
```shell
sysctl -n hw.ncpu
```

How can I get the list of most recently modified 50 files under the current directory (recursively)?
```shell
find . -type f -print0 | xargs -0 stat --format '%Y :%y %n' | sort -nr | cut -d: -f2- | head -n 50
```

How can I make my Linux system set the hardware clock to "local" time (in order to fix system time conflicts for my dual-boot setup)?
```shell
timedatectl set-local-rtc 1
```

## Byobu

### Byobu with tmux back end

How can I start a new Byobu session with a specified name?
```shell
byobu new -s <session-name>
````

How can I rename an existing Byobu session?
```shell
byobu rename -t <session-name> <new-session-name>
```

## Celery

How should I start the Celery worker process for a Django project in the development environment?
```shell
# $PROJECT_DIRECTORY is the absolute path for the Django project
# (same path with the manage.py file)
cd $PROJECT_DIRECTORY
celery -A $PROJECT_NAME worker -l info
```

## GitHub

How can I change the author information on a project historically?
- Refer to [GitHub's documentation](https://help.github.com/articles/changing-author-info/).
