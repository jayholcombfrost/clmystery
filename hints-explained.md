## Hint Walk-through

1. `git clone https://github.com/veltman/clmystery.git`
1. Navigate to `mystery` directory
1. Take a quick look at each of the files in there to get a sense of what data they contain by using `head`:
    1. Search for all of the clues: `grep CLUE crimescene` (3 results)
1. The 3rd clue is a witness, whose address you can find by searching the file called "people": 
    1. `grep Annabel people` (4 results)
1. Since we know Annabel is a woman, we need investigate only 2 of the 4 results
1. For each of those two, look up their street in the "Street" index file. You should receive an interview number. The following command uses `head` to capture all of the lines up to that number, then appends `tail` to show the last line number of that selection
    1. `head -n 179 streets/Buckingham_Place | tail -n 1` // SEE INTERVIEW #699607
    1. `head -n 40 streets/Hart_Place | tail -n 1` // SEE INTERVIEW #47246024
1. In the right interview, we learn that the getaway vehicle was a *Honda*, with a license plate that starts with "L337" and ends with "9", so now we move to the Vechiles file.
1. Grepping simply for any of the terms we picked up from the interview won't help, so we need a new trick: `grep -A` which allows you to return a certain number of lines after the result.
1. However, which term should we grep? "Honda", "Blue", or "L337". 
    1. I ran a quick `grep -c` to display the number ("count") of each term. 
    1. "L337" is the smallest number of results: `grep -A 5 "L337" vehicles`
1. Now by looking through the 13 results and manually noting Blue Hondas where the owner is over 6', we get the following names:
    1. Erika Owens
    1. Joe Germuska
    1. Jeremy Bowers
    1. Jacqui Maher
1. Since the suspect was reported to be a man, we can eliminate the feminine names as suspects. 
1. At this point, we could just run the solution. But let's do the last hint, which shows us how to search through multiple files
1. Since we know which membership cards the suspect had, it'd be good to grep for a name across multiple files at once. This can be done with `cat`: 
    1. `cat AAA Delta_SkyMiles Museum_of_Bash_History | grep Joe`
1. Now we should have a clear idea of what the answer is. Let's run the solution script to see: 
    1. `echo "John Doe" | $(command -v md5 || command -v md5sum) | grep -qif /dev/stdin encoded && echo CORRECT\! GREAT WORK, GUMSHOE. || echo SORRY, TRY AGAIN.`


## Commands:

`grep [term] [filename]`
search for a term in a file

`grep -A 5 [term] [filename]`
search for a term in a file and display the 5 lines after each result

`grep -B 5 [term] [filename]`
search for a term in a file and display the 5 lines before each result


`head [filename]`
`tail [filename]`
shows you the first/last 10 lines of a file

`head -n 30 [filename]` 
`tail -n 30 [filename]` 
shows you the first/last 30 lines of a file
