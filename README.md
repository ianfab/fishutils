# fishutils
Auto-apply parameter tweaks to [Stockfish](https://github.com/official-stockfish/Stockfish) or [multi-variant Stockfish](https://github.com/ddugovic/Stockfish).

## Usage
Run `python fishutils.py -h` to get info on required and optional arguments.

The main functionality of the script is to automatically apply SPSA tuning results from [fishtest](https://github.com/glinscott/fishtest) or [multi-variant fishtest](https://github.com/ianfab/fishtest) to your Stockfish repository. To do this, copy the results of a SPSA tuning session to a file and run `python fishutils.py -s /path/to/stockfish/src/ -i /path/to/tuning_results.txt`, or copy the the tuning results to the clipboard and run `python fishutils.py -s /path/to/stockfish/src/` and then insert them.

A line of the tuning results could, e.g., look like:
`param: mLever[4], best: 27.00, start: 17.00, min: -100.00, max: 200.00, c 41.714131, a 223.069148`.

If you want to see which changes would be applied without actually writing them to files, then you can use the `-d/--dry-run` option.
