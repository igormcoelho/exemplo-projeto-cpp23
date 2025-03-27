# exemplo-projeto-cpp23

*Exemplo de Projeto em C++23*

## Organização do Código

Assumimos uma pasta `src/` contendo o arquivo `exemplo.cpp` abaixo:

```.cpp
import std;
using namespace std;

auto main() -> int {
  println("Ola Mundo!");
  return 0;
}
```

E crie um CMakeLists.txt na raiz do projeto, que explicará ao compilador como compilar o projeto:

```
cmake_minimum_required(VERSION 4.0.0)
# set(CMAKE_CXX_COMPILER /usr/bin/g++-15)
set(CMAKE_CXX_COMPILER /usr/bin/clang++-19)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_EXPERIMENTAL_CXX_IMPORT_STD "a9e1cf81-9932-4810-974b-6eccaf14e457")

set(CMAKE_CXX_MODULE_STD 1)

project(projeto_exemplo_cpp23 VERSION 0.1.0 LANGUAGES CXX)

add_executable(exemplo_cpp23 src/exemplo.cpp)
```

Os caminhos relativos dos compiladores podem necessitar de modificação no CMakeLists.txt, bem como a passagem da biblioteca libc++, caso outro compilador seja utilizado, diferentemente do Clang.
Observamos também que, no `CMakeLists.txt`, o uso de hashtag (`#`) significa comentar a linha após esse ponto, assim como em Python.

## Ferramentas Necessárias

Basicamente, assumimos um compilador C++ instalado, também o sistema de construção (build) CMake 4.0 e Ninja.

- Felizmente, o CMake 4.0.0-rc5 já está disponível para download e instalação no site do CMake: https://cmake.org/download/ 

Como compilador, assumimos o Clang 19 ou superior, pois ele também vem com demais ferramentas importantes do LLVM 19, como clang-format (formatador de código), clang-tidy (linter/static checker) e clangd (suporte de CompileCommands.json para IDE).

Assumimos também a instalação do Visual Studio Code, SEM A EXTENSÃO PADRÃO C/C++ DA MICROSOFT:

- desinstale a extensão `ms-vscode.cpptools-extension-pack`
- instale a extensão do LLVM `llvm-vs-code-extensions.vscode-clangd`
- instale a extensão do CMake `ms-vscode.cmake-tools`

## Resultado Esperado com VSCode

No VSCode, a extensão do CMake deve fazer aparecer no Menu Inferior um botão de "Compilar" e um "play" (triangulo invertido) para executar.

O comando de Compilar deve dar o seguinte resultado:

```
[main] Compilando a pasta: /SEU_CAMINHO_NO_SISTEMA/exemplo-projeto-cpp23/build 
[build] Iniciando o build
[proc] Executando o comando: /SEU_CAMINHO_NO_SISTEMA/.local/bin/cmake --build /SEU_CAMINHO_NO_SISTEMA/exemplo-projeto-cpp23/build --config Debug --target all --
[build] [2/8  12% :: 0.028] Generating CXX dyndep file CMakeFiles/__cmake_cxx23.dir/CXX.dd
[build] [2/5  40% :: 0.072] Scanning /SEU_CAMINHO_NO_SISTEMA/exemplo-projeto-cpp23/src/exemplo.cpp for CXX dependencies
[build] [3/5  60% :: 0.078] Generating CXX dyndep file CMakeFiles/exemplo_cpp23.dir/CXX.dd
[build] [4/5  80% :: 1.218] Building CXX object CMakeFiles/exemplo_cpp23.dir/src/exemplo.cpp.o
[build] [5/5 100% :: 1.346] Linking CXX executable exemplo_cpp23
[driver] Build concluído: 00:00:01.383
[build] Build concluído com o código de saída 0
```

Ao executar, o seguinte resultado será esperado:

```
Ola Mundo!
```

## Compilar com CMake sem VSCode

Sem o VSCode, para compilar manualmente com CMake e Ninja, basta executar os seguintes comandos:

(TENHA MUITO CUIDADO COM O COMANDO DE REMOÇÃO DA PASTA build/ A SEGUIR!!!)

```
$ rm -rf build/ && mkdir -p build/
$ cd build
$ cmake .. -GNinja && ninja
```

E para executar, basta:

```
$ ./exemplo_cpp23 
Ola Mundo!
```

## Licença

MIT

Igor Machado Coelho, 2025
