This codebook gives details on how to interpret the data fields (columns) in the `part1_data.csv` file.

| Column name   | Description | Values |
| ------------: | :---: | :---: |
| `id`          | An ID code that uniquely identifyies each participant | Alphanumeric string, e.g., `1g0kwzt5fqv3p1zms87j2y2g` |
| `block`       | Block number within the task | Integer: `1` or `2` |
| `trial`       | Trial number within a block | Integer between `1` and `48`              |
| `left_stim`   | Stimulus displayed on the left in this trial | Integer (0-indexed) between `0` and `3`. A value of `-1` means that no stimulus was displayed on the left.   |
| `right_stim`  | Stimulus displayed on the right in this trial | Integer (0-indexed) between `0` and `3`. A value of `-1` means that no stimulus was displayed on the right. |
| `chosen_stim` | Stimulus chosen by the participant | Integer (0-indexed) between `0` and `3`. A value of `-1` means that no stimulus was chosen.                            |
| `payout`      | Reward received by the participant | Boolean: a reward either was (`1`) or was not (`0`) received. |
| `choice`      | Whether choice was for the left or right stimulus | String: `left` or `right`. |
| `trial_type`  | Indicates whether trial was free-choice (2 choice options available) or forced-choice (only 1 choice option available) | String: `free` or `forced`. |
