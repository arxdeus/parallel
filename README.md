# Parallel

An action that allows you to run an unlimited (probably) number of commands in parallel

## Usage

```yaml
- name: Parallel task execution
    uses: arxdeus/parallel@v1
    with:
        commands: |
        - first_command: mkdir test1
        - second_command: mkdir test2
        ...
        - infinite_command: mkdir test9999
```

`commands` accepts any number of steps in format:
` - [command_name]: [command_call] (bash)`

`[command_name]` will be reported if the step fails (it doesn't interrupt the execution of other steps)

### Example step for parallel dart code check and analysis

You may adapt it to you own requirements

```yaml
- name: Run tests parallel
    uses: arxdeus/parallel@v1
    with:
        commands: |
        - format: find lib test -name "*.dart" ! -name "*.*.dart" -print0 | xargs -0 dart format --set-exit-if-changed --line-length 100
        - analyze: dart analyze --fatal-infos --fatal-warnings
        - tests: dart --enable-vm-service test --file-reporter="json:${{ github.workspace }}/flutter-test-report.json" --concurrency=6
```
