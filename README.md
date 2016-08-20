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
