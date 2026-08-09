### 9x9 multiple table
```bash
seq 1 9 | awk '{for(j=1;j<=$1;j++) printf "%d×%d=%-2d ", j, $1, j*$1; print ""}'
```
### Pascal's triangle
```bash
N=9
seq 0 "$N" | awk -v N="$N" '
{
    for (i = 0; i < N - $1; i++)
        printf "  "

    c = 1
    for (k = 0; k <= $1; k++) {
        printf "%-5d", c
        c = c * ($1 - k) / (k + 1)
    }
    print ""
}'
```
