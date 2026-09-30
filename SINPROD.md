# FlameRobin - fork SINPROD

Fork de https://github.com/mariuz/flamerobin (licenca MIT, ver `LICENSE`) mantido
pela organizacao admlsinprod para consulta e administracao de bancos Firebird
(sinpdados, BASESQL, base de clientes).

## Branches e remotos

| Remoto | URL | Uso |
|---|---|---|
| `origin` | https://github.com/admlsinprod/flamerobin | nosso fork |
| `upstream` | https://github.com/mariuz/flamerobin | projeto original |

- `master`: espelho do upstream. Nao receber commit proprio.
- `sinprod`: branch de trabalho, com os ajustes da SINPROD.
- Ajustes de interesse geral: branch a partir de `master`, PR para o upstream.

Trazer novidades do upstream:

```bash
git fetch upstream
git checkout master && git merge --ff-only upstream/master && git push origin master
git checkout sinprod && git merge master
```

## Build no Windows (resumo)

Detalhes completos em `BUILD.md`. Requisitos: Visual Studio 2022 (C++), CMake 3.18+,
Git. As dependencias (wxWidgets, Boost, cliente Firebird 5.0.x, fb-cpp) vem do vcpkg
em modo manifest.

```cmd
git clone --recursive https://github.com/admlsinprod/flamerobin.git
cd flamerobin
git checkout sinprod
git clone https://github.com/microsoft/vcpkg vcpkg
vcpkg\bootstrap-vcpkg.bat
cmake -S . -B build -A x64
cmake --build build --config Release
```

A primeira configuracao compila as dependencias e demora. Sempre usar diretorio
`build` limpo ao reconfigurar. Se faltar o pacote `fb-cpp`, o toolchain do vcpkg nao
foi ativado (ver "Troubleshooting" no `BUILD.md`).

## Pendencias de validacao (nada disso foi testado ainda)

- Conectar na sinpdados e na BASESQL (Firebird 5, `192.168.0.151`).
- Comportamento com SQL Dialect 1 (a base do SINPROD usa Dialect 1).
- Charset/acentuacao (WIN1252) em consultas e resultados.
- Definir onde publicar o executavel para o time.
