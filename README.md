# JaperCoin Core

**JaperCoin (JAP)** es una moneda igual que Bitcoin, pero el doble de mejor.
Es un fork legal del código abierto de **Bitcoin Core v30.4** (commit
`5cd4411`), con el nombre y la red propios, bajo licencia MIT.
Premine: **0**.

> **English summary:** JaperCoin (JAP) is a legal fork of Bitcoin Core v30.4
> (commit `5cd4411`), MIT licensed, with its own name and network.
> 5-minute blocks, 42,000,000 max supply, 50 JAP block reward, halving every
> 420,000 blocks, SHA-256 proof of work, BIP94 anti-timewarp from genesis,
> SegWit and Taproot active from block 1. Premine: 0.
> 1 JAP = 100,000,000 coques. P2P port 9433, RPC port 9432,
> bech32 addresses `jap1q...`.
> Genesis hash: `0000000010b4eca4e4962faac3f451f2e319b49cb793ffed76ffb66b7899248b`.

---

## ¿Qué es JaperCoin?

JaperCoin es una criptomoneda con su propia cadena de bloques, basada en el
código abierto de Bitcoin Core. No es un token de otra cadena: tiene su
propia red, sus propios nodos y su propio minado por prueba de trabajo
(SHA-256, la misma que Bitcoin, así que cualquier minero de Bitcoin sirve).

La regla del proyecto: **Bitcoin 100%, JaperCoin 200%**. Todo lo que se
mejoró respecto a Bitcoin está verificado en el código y documentado abajo.
Nada se inventó fuera del estudio del código de Bitcoin Core.

## Parámetros

| Parámetro | Bitcoin | JaperCoin |
|---|---|---|
| Nombre / símbolo | Bitcoin / BTC | **JaperCoin / JAP** |
| Tiempo de bloque | 10 min | **5 min (300 s)** |
| Suministro máximo | 21,000,000 | **42,000,000** |
| Recompensa inicial | 50 BTC | **50 JAP** |
| Halving | cada 210,000 bloques | **cada 420,000 bloques (~4 años)** |
| Ajuste de dificultad | cada 2,016 bloques / 2 semanas | **cada 2,016 bloques / 1 semana** |
| Peso máximo de bloque | 4,000,000 WU | **4,000,000 WU** |
| Prueba de trabajo | SHA-256 | **SHA-256** |
| Madurez de coinbase | 100 bloques | **100 bloques** |
| Comisión mínima | 1 sat/vB | **1 coque/vB** |
| BIP94 anti-timewarp | NO (en mainnet) | **SÍ, desde el génesis** |
| SegWit | desde el bloque 481,824 | **desde el bloque 1** |
| Taproot | desde el bloque 709,632 | **desde el bloque 1** |
| Confirmaciones recomendadas | 6 (~1 h) | **12 (~1 h)** |
| Emisión termina | ~año 2140 | **~año 2158** |
| Máx. transacciones/seg | ~7 | **~14** |
| Preminado | 0 | **0** |
| Puerto P2P mainnet | 8333 | **9433** |
| Puerto RPC mainnet | 8332 | **9432** |
| Magic bytes mainnet | `f9beb4d9` | **`4a1cb5f9`** |
| Direcciones P2PKH | empiezan con `1` | **empiezan con `C`** (prefijo 28) |
| Direcciones P2SH | empiezan con `3` | **empiezan con `5`** (prefijo 10) |
| Claves privadas (WIF) | empiezan con `5`/`K`/`L` | **empiezan con `Q`** (prefijo 156) |
| Claves extendidas | `xpub`/`xprv` | **`jpub`/`jprv`** |
| Bech32 (SegWit/Taproot) | `bc1q…` | **`jap1q…`** |
| Nombre del cliente | Bitcoin Core | **JaperCoin Core v1.0.0** |
| Archivo de configuración | `bitcoin.conf` | **`japercoin.conf`** |
| Directorio de datos | `~/.bitcoin` | **`~/.japercoin`** |

### La unidad chica: el coque

La unidad pequeña de JaperCoin se llama **coque** (singular) / **coques**
(plural), igual que el satoshi de Bitcoin.

- **1 JAP = 100,000,000 coques** (1 coque = 0.00000001 JAP).
- La recompensa inicial de 50 JAP por bloque son 5,000,000,000 coques.
- La comisión mínima es de 1 coque por byte virtual.

### Bloque génesis

- **Mensaje:** `JaperCoin 17/Nov/2026 El doble de mejor que Bitcoin`
- **Hash del génesis:**
  `0000000010b4eca4e4962faac3f451f2e319b49cb793ffed76ffb66b7899248b`
- **Merkle root:**
  `00a405266cd51cd60bf12635b8d2b1e0e2cdcd6d5c3f7d99e8cec66978e5cafa`
- **nBits:** `0x1d007fff` (dificultad 2)
- **nTime / nNonce:** `1794922438` / `2013369718`

### Premine: 0

En el código no hay ninguna moneda reservada para nadie: ni para el creador,
ni para un equipo, ni para un fondo. Exactamente como Bitcoin: la única forma
de crear monedas es minando bloques, 50 JAP por bloque al inicio, con halving
cada 420,000 bloques. Los 50 JAP del bloque génesis **no se pueden gastar
nunca**, igual que los 50 BTC del génesis de Bitcoin.

### Qué se mejoró respecto a Bitcoin (verificado en el código)

1. **Ataque timewarp cerrado:** BIP94 activo desde el génesis en las 4 redes.
   Bitcoin mainnet aún lo permite.
2. **Ajuste de dificultad cada 7 días** (2,016 bloques) en vez de 14 días.
3. **Bloques cada 5 minutos:** 12 confirmaciones ≈ 1 hora.
4. **SegWit y Taproot activos desde el bloque 1**, no años después.
5. **BIP34/65/66/CSV activos desde el bloque 1.**
6. **Excepciones históricas de script eliminadas:** no aplican a una cadena nueva.
7. **Génesis con dificultad 2** (`0x1d007fff`) para mitigar el instamine.
8. **Datos de Bitcoin embebidos a cero / al génesis propio**
   (`nMinimumChainWork = 0`, `defaultAssumeValid` = hash del génesis,
   `chainTxData = {0,0,0}`).
9. **Identidad de red propia y verificada sin colisión:** magic `4a1cb5f9`,
   puertos 9433/9432, prefijos 28/10/156, bech32 `jap`, `jpub`/`jprv`.
10. **Premine 0** y génesis no gastable.

Límites honestos: la seguridad de una cadena pequeña depende de que haya
mineros reales; con poco hashrate existe riesgo de ataque del 51% (como les
pasó a Bitcoin Gold en 2018/2020 y a Bitcoin SV en 2021). La defensa a medio
plazo en estudio es la minería fusionada (merge-mining) con Bitcoin. Además
faltan todavía: nodos semilla propios, explorador de bloques y billetera para
usuarios.

## Cómo compilar

En Ubuntu/Debian, con las dependencias de Bitcoin Core ya instaladas (ver
[`doc/build-unix.md`](doc/build-unix.md) de Bitcoin Core para la lista
completa de dependencias):

```bash
cmake -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_IPC=OFF -DBUILD_TESTS=OFF \
  -DBUILD_GUI=OFF -DBUILD_BENCH=OFF -DBUILD_FUZZ_BINARY=OFF
cmake --build build -j2 --target bitcoind bitcoin-cli
```

`-j2` por la RAM limitada de la máquina virtual. La primera compilación tarda
varias horas; las siguientes son incrementales (minutos). La interfaz gráfica
no se compila en esta versión; el nodo es por línea de comandos.

## Cómo correr un nodo

```bash
# Mainnet de JaperCoin (puerto P2P 9433, RPC 9432)
./build/src/bitcoind -datadir=~/.japercoin -daemon

# Ver que está corriendo y en qué altura va
./build/src/bitcoin-cli -datadir=~/.japercoin getblockcount
./build/src/bitcoin-cli -datadir=~/.japercoin getblockchaininfo

# Pararlo
./build/src/bitcoin-cli -datadir=~/.japercoin stop
```

Para que otros nodos se conecten, el puerto 9433 debe estar abierto y el nodo
debe conocer a otro nodo (`-addnode=<IP>:9433`). Hoy no hay nodos semilla:
dos nodos se conectan entre sí con `-addnode`.

## Cómo minar

Bitcoin Core v30.4 no trae minero integrado. El flujo es `getblocktemplate`
→ minero externo → `submitblock`:

```bash
# 1. Crear billetera y dirección para cobrar
bitcoin-cli -datadir=~/.japercoin createwallet minero
bitcoin-cli -datadir=~/.japercoin getnewaddress   # dirección jap1q...

# 2. Pedir plantilla de bloque (con la dirección como coinbase)
bitcoin-cli -datadir=~/.japercoin getblocktemplate '{"rules":["segwit"]}'

# 3. Construir la coinbase con esa plantilla (altura, recompensa,
#    scriptPubKey, compromiso witness SegWit) y minar la cabecera con
#    un minero SHA-256 que acepte cabecera de 80 bytes

# 4. Enviar el bloque
bitcoin-cli -datadir=~/.japercoin submitblock <bloque_en_hex>
```

Con CPU normal, un bloque de mainnet (dificultad 2) tarda del orden de media
hora; con un ASIC de Bitcoin, segundos (la prueba de trabajo es SHA-256, la
misma que Bitcoin, así que cualquier minero de Bitcoin sirve). Las monedas
minadas maduran a los 100 bloques.

## Cómo mandar monedas

```bash
# En el nodo que tiene monedas maduras (100 bloques después de minarlas)
bitcoin-cli -datadir=~/.japercoin sendtoaddress <direccion_jap1q...> 10

bitcoin-cli -datadir=~/.japercoin getbalance
```

## Redes de prueba

| Red | Puerto P2P | Puerto RPC | Magic | Bech32 |
|---|---|---|---|---|
| mainnet | 9433 | 9432 | `4a1cb5f9` | `jap` |
| testnet3 | 19433 | 19432 | `a2a9a228` | `tjap` |
| testnet4 | 49433 | 49432 | `71ab6e17` | `tjap` |
| signet | 39433 | 39432 | (el de Bitcoin signet, génesis propio no cambiado) | `sjap` |
| regtest | 19444 | 19443 | `8be6654a` | `japrt` |

## Sitio web y explorador

- Sitio web oficial: próximamente.
- Explorador de bloques: próximamente.

## Licencia y atribución

JaperCoin Core es un fork de **Bitcoin Core v30.4** (commit `5cd4411`),
licencia **MIT**. Ver [`COPYING`](COPYING).

Bitcoin Core es software libre bajo la licencia MIT; JaperCoin hereda esa
licencia y mantiene la atribución a sus autores originales. Los cambios
propios de JaperCoin (parámetros de red, génesis, prefijos, puertos y marca)
están documentados en los archivos `src/kernel/chainparams.cpp`,
`src/chainparamsbase.cpp`, `src/chainparamsseeds.h`, `src/common/args.cpp`,
`src/consensus/amount.h`, `src/validation.cpp` y `CMakeLists.txt`.

## Seguridad

Si encuentras una vulnerabilidad, repórtala de forma responsable siguiendo
[`SECURITY.md`](SECURITY.md) (heredado de Bitcoin Core).

**Advertencia:** JaperCoin nace con valor cero, sin nodos semilla propios
todavía, sin explorador de bloques y sin listados en casas de cambio. No hay
ninguna promesa de precio ni de listado. Listar no crea el precio: el precio
lo pone el mercado.
