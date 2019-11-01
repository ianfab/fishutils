# fishutils
Auto-apply parameter tweaks to [Stockfish](https://github.com/official-stockfish/Stockfish) or [multi-variant Stockfish](https://github.com/ddugovic/Stockfish).

## Usage
Run `python3 fishutils.py -h` to get info on required and optional arguments. See the [Wiki](https://github.com/ianfab/fishutils/wiki) for a simple example on how to use the script.

The main functionality of the script is to automatically apply SPSA tuning results from [fishtest](https://github.com/glinscott/fishtest) or [multi-variant fishtest](https://github.com/ianfab/fishtest) to your Stockfish repository. To do this, copy the results of a SPSA tuning session to a file and run `python3 fishutils.py -s /path/to/stockfish/src/ -i /path/to/tuning_results.txt`, or copy the the tuning results to the clipboard and run `python3 fishutils.py -s /path/to/stockfish/src/` and then insert them.

An input line for the script (taken from fishtest tuning results) can, e.g., look like:
`param: mLever[4], best: 27.00, start: 17.00, min: -100.00, max: 200.00, c 41.714131, a 223.069148`. The script then changes the value in the source code according to the given input line, in this example changing the middlegame value of `Lever[4]` from 17 to 27.

### Features
- Types `int`, `Value`, and `Score` are supported.
- Enums are replaced by their values when used as an array index, e.g., `[PAWN]` -> `[1]`.
- If a variable is defined by an enum, the tuning results are applied to the defining enum instead of the variable itself, e.g., `PieceValue[MG][1]` -> `PawnValueMg`.
- The functions `round`, `floor`, and `ceil` are supported for rounding the best/new value.
- The `-d/--dry-run` option can be used to view the changes wihout applying them to files.
- Replacing values might lead to misaligned lines of array definitions. These can be realigned by running the script with the option `-m align` afterwards.

### Limitations
The script does not parse C++ code, but only searches for regular expression patterns. Therefore, it might fail to apply tuning results due to:
- comments
- preprocessor directives
- namespaces
- conflicting names/definitions
