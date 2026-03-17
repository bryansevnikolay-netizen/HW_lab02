## Laboratory work II

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
```// do it on web-github
```
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
```
$ echo "# HW-lab02" >> README.md
$ git init >> file1 2>&1
$ git add README.md >> file1 2>&1
$ git commit -m "first commit" >> file1 2>&1
$ git branch -M main >> file1 2>&1
$ git remote add origin https://github.com/bryansevnikolay-netizen/HW-lab02.git >> file1 2>&1
$ git push -u origin main >> file3 2>&1
```
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```
cat > hello_world.cpp << 'EOF'
/*
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
EOF
*/
```
4. Добавьте этот файл в локальную копию репозитория.
```
$ git add hello_world.cpp >> file1 2>&1
```
5. Закоммитьте изменения с *осмысленным* сообщением.
```
$ git commit -m "Add hello_world.cpp" >> file1 2>&1
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```
cat > hello_world.cpp << 'EOF'
/*
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello world from " << name << endl;
    return 0;
}
EOF
*/
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
```
$ git commit -m "Add updated hello_world.cpp" >> file1 2>&1
// we don`t use "git add" because this file is already being tracked by GitHub
```
8. Запуште изменения в удалёный репозиторий.
```
$ git push -u origin main >> file1 2>&1
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
```
// history is accessed
```
### Part II

1. В локальной копии репозитория создайте локальную ветку `patch1`.
``` 
$ git checkout -b patch1 >> file2 2>&1
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```
cat > hello_world.cpp << 'EOF'
/* 
include <iostream>
include <string>
int main() {
std::string name;
std::cout << "Please enter name";
std::cin >> name;
std::cout << "Hello world from " << name;
return 0;
}
EOF
*/
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```
$ git add hello_world.cpp >> file2 2>&1
$ git commit -m "patched hello_world.cpp" >> file2 2>&1
$ git push origin patch1 >> file2 2>&1
```
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
```
// patch1 is accessed
```
5. Создайте pull-request `patch1 -> master`.
```
// pull-request was created
```
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
```
$ git add hello_world.cpp >> file2 2>&1
/*
#include <iostream>
#include <string>

int main() {
std::string name;
// comment
std::cout << "Please enter name";
std::cin >> name;
std::cout << "Hello world from " << name;
return 0;
}
EOF
*/
```
7. **commit**, **push**.
```
$ git add hello_world.cpp >> file2 2>&1
$ git commit -m "added comment" >> file2 2>&1
$ git push origin patch1 >> file2 2>&1
```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
```
// changes were created
```
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
```
// merge was made on web-GitHub
```
10. Локально выполните **pull**.
```
$ git checkout main >> file2 2>&1
$ git pull origin main >> file2 2>&1
```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```
$ git log >> file2 2>&1
```
12. Удалите локальную ветку `patch1`.
```
$ git branch -d patch1 >> file2 2>&1
```

### Part III

1. Создайте новую локальную ветку `patch2`.
``` 
$ git checkout -b patch2 >> file3 2>&1
```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```
& clang-format hello_world.cpp -style=Mozilla -i hello_world.cpp >> file3 2>&1
/*
#include <iostream>
#include <string>

int
main()
{
  std::string name;
  // comment
  std::cout << "Please enter name";
  std::cin >> name;
  std::cout << "Hello world from " << name;

  return 0;
}
*/
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```
$ git add hello_world.cpp >> file3 2>&1
$ git commit -m "Update Mozilla code style with clang-format" >> file3 2>&1
$ git push origin patch1 >> file3 2>&1
// pull-request was created
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```
$ git checkout main >> file3 2>&1
$ nano hello_world.cpp
*/
#include <iostream>
#include <string>

int main() {
    std::string name;
    // only comment no more
    std::cout << "Please enter name";
    std::cin >> name;
    std::cout << "Hello world from " << name;
}
*/
$ git add hello_world.cpp >> file3 2>&1
$ git commit -m "Change comments" >> file3 2>&1
$ git push origin main >> file3 2>&1
```
5. Убедитесь, что в pull-request появились *конфликтны*.
```
$ git checkout patch2 >> file3 2>&1
$ git pull --rebase origin main >> file3 2>&1
// conflicts was appeared in PR
```
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```
/*
#include <iostream>
#include <string>

<<<<<<< HEAD
int main() {
    std::string name;
  // only comment no more
std::cout << "Please enter name";
    std::cin >> name;
    std::cout << "Hello world from " << name;
=======
int
main()
{
  std::string name;
  // comment
  std::cout << "Please enter name";
  std::cin >> name;
  std::cout << "Hello world from " << name;

  return 0;
*/
$ nano hello_world.cpp
// solving conflicts with unification of wariant hello_world.cpp
// after unification
/*
#include <iostream>
#include <string>

int main() {
  std::string name;
  // only comment no more
  std::cout << "Please enter name";
  std::cin >> name;
  std::cout << "Hello world from " << name;

  return 0;
}
*/
$ git add hello_world.cpp >> file3 2>&1
$ git status >> file3 2>&1
// conflict was solved
$ git rebase --continue >> file3 2>&1
```
7. Сделайте *force push* в ветку `patch2`
```
$ git push --force-with-lease origin patch2
```
8. Убедитель, что в pull-request пропали конфликтны. 
```
// no conflicts
```
9. Вмержите pull-request `patch2 -> master`.
```
$ merge patch2 >> file3 2>&1
```
