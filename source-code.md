# WORDLE ALGORITHM WARS : ITERATIVE vs. RECURSIVE

### 2311102182 MUTIA RANI ZAHRA MEILANI 
### 2311102279 NATASYA INTAN SUKMA JIWANTI

```go
package main

import (
	"fmt"
	"math/rand"
	"strings"
	"time"
)

var words = []string{
    "apple", "table", "chair", "water", "stone",
    "house", "tiger", "light", "dance", "dream",
    "peach", "money", "smile", "green", "beach",
    "fruit", "grass", "shirt", "world", "paper",
    "night", "cloud", "bread", "drink", "glass",
    "flows", "music", "phone", "carol", "laugh",
    "block", "heart", "sugar", "round", "quick",
    "straw", "clean", "power", "sharp", "tired",
    "jambu", "sweat", "muddy", "aster", "pearl",
    "paint", "brush", "growl", "steel", "shark",
    "horse", "sleep", "leafs", "baker", "trick",
    "minty", "gravy", "spade", "sweep", "stack",
    "punch", "shoty", "crook", "reach", "shore",
    "flame", "great", "misty", "pinky", "twirl",
    "crash", "gates", "milky", "fresh", "bossy",
    "horny", "leafy", "hurts", "glowy", "drear",
    "giddy", "ocean", "jolly", "plain", "softy",
    "randy", "pitch", "tasty", "dusty", "sandy",
    "chill", "crazy", "blank", "shaky", "lucky",
    "fuzzy", "madly", "spicy", "honey", "curvy",
    "berry", "lover", "angel", "zesty", "syrup",
    "bloom", "feast", "grape", "sharp", "bliss",
    "froze", "fetch", "mango", "raven", "flare",
    "plush", "vivid", "folly", "charm", "piano",
    "vocal", "sight", "noble", "fiery", "crown",
    "brave", "shiny", "novel", "risky", "spark",
    "dizzy", "quirk", "moody", "gloom", "timid",
    "lunar", "brisk", "hound", "jolly", "vault",
    "candy", "pearl", "truce", "diver", "sleek",
    "match", "frost", "gleam", "token", "blaze",
    "quest", "eager", "chess", "flock", "cedar",
    "maple", "amber", "valor", "haven", "prism",
    "trend", "silky", "flare", "siren", "azure",
    "pivot", "glare", "proud", "rover", "serif",
    "mirth", "grove", "witty", "gamer", "fetch",
    "blurt", "rogue", "swirl", "flint", "crisp",
    "clerk", "sheer", "wound", "scout", "vigor",
    "knack", "dwell", "frail", "gland", "spore",
    "shrub", "fluke", "chant", "mirth", "glean",
    "probe", "fable", "troop", "vivid", "flick",
}
	
var guesses = []string{
    "apple", "table", "chair", "water", "stone",
    "house", "tiger", "light", "dance", "dream",
    "peach", "money", "smile", "green", "beach",
    "fruit", "grass", "shirt", "world", "paper",
    "night", "cloud", "bread", "drink", "glass",
    "flows", "music", "phone", "carol", "laugh",
    "block", "heart", "sugar", "round", "quick",
    "straw", "clean", "power", "sharp", "tired",
    "jambu", "sweat", "muddy", "aster", "pearl",
    "paint", "brush", "growl", "steel", "shark",
    "horse", "sleep", "leafs", "baker", "trick",
    "minty", "gravy", "spade", "sweep", "stack",
    "punch", "shoty", "crook", "reach", "shore",
    "flame", "great", "misty", "pinky", "twirl",
    "crash", "gates", "milky", "fresh", "bossy",
    "horny", "leafy", "hurts", "glowy", "drear",
    "giddy", "ocean", "jolly", "plain", "softy",
    "randy", "pitch", "tasty", "dusty", "sandy",
    "chill", "crazy", "blank", "shaky", "lucky",
    "fuzzy", "madly", "spicy", "honey", "curvy",
    "berry", "lover", "angel", "zesty", "syrup",
    "bloom", "feast", "grape", "sharp", "bliss",
    "froze", "fetch", "mango", "raven", "flare",
    "plush", "vivid", "folly", "charm", "piano",
    "vocal", "sight", "noble", "fiery", "crown",
    "brave", "shiny", "novel", "risky", "spark",
    "dizzy", "quirk", "moody", "gloom", "timid",
    "lunar", "brisk", "hound", "jolly", "vault",
    "candy", "pearl", "truce", "diver", "sleek",
    "match", "frost", "gleam", "token", "blaze",
    "quest", "eager", "chess", "flock", "cedar",
    "maple", "amber", "valor", "haven", "prism",
    "trend", "silky", "flare", "siren", "azure",
    "pivot", "glare", "proud", "rover", "serif",
    "mirth", "grove", "witty", "gamer", "fetch",
    "blurt", "rogue", "swirl", "flint", "crisp",
    "clerk", "sheer", "wound", "scout", "vigor",
    "knack", "dwell", "frail", "gland", "spore",
    "shrub", "fluke", "chant", "mirth", "glean",
    "probe", "fable", "troop", "vivid", "flick",
}

func playIterative(target string, guesses []string, maxAttempts int) int {
	for i := 0; i < maxAttempts; i++ {
		guess := guesses[i]
		fmt.Printf("TEBAKAN %d : %s - %s\n", i+1, guess, feedback(guess, target))
		if guess == target {
			fmt.Println("YEEY! KAMU BERHASIL MENEBAK")
			return i + 1
		}
	}
	fmt.Println("KATA YANG BENAR :", target)
	return maxAttempts
}

func playRecursive(target string, guesses []string, attempt, maxAttempts int) int {
	if attempt >= maxAttempts {
		fmt.Println("KATA YANG BENAR :", target)
		return maxAttempts
	}

	guess := guesses[attempt]
	fmt.Printf("TEBAKAN %d : %s - %s\n", attempt+1, guess, feedback(guess, target))
	if guess == target {
		fmt.Println("YEEY! KAMU BERHASIL MENEBAK.")
		return attempt + 1
	}

	return playRecursive(target, guesses, attempt+1, maxAttempts)
}

func feedback(guess, target string) string {
	result := strings.Builder{}
	for i := 0; i < len(guess); i++ {
		switch {
		case guess[i] == target[i]:
			result.WriteByte('g')
		case strings.Contains(target, string(guess[i])):
			result.WriteByte('y')
		default:
			result.WriteByte('b')
		}
	}
	return result.String()
}

func main() {
    // INISIALIASI SEED
    rand.Seed(time.Now().UnixNano())
    
    // MENCARI TARGET WORD SECARA ACAK
	targetWord := words[rand.Intn(len(words))]
	
	// MENGACAK URUTAN GUESSES
	rand.Shuffle(len(guesses), func(i, j int) {
		guesses[i], guesses[j] = guesses[j], guesses[i]
	})
	
	// GUI
	fmt.Println("WELCOME TO WORDLE!")
	fmt.Println("'g': HURUF DAN POSISI BENAR!")
	fmt.Println("'y': ADA HURUFNYA! TETAPI POSISINYA SALAH")
	fmt.Println("'b': TIDAK ADA HURUF INI!")

	// Pendekatan Rekursif
	fmt.Println("\nREKURSIF")
	start := time.Now()
	attemptsRecursive := playRecursive(targetWord, guesses, 0, 10)
	durationRecursive := time.Since(start).Seconds()
	
	// Pendekatan Iteratif
	fmt.Println("\nITERATIF")
	start = time.Now()
	attemptsIterative := playIterative(targetWord, guesses, 10)
	durationIterative := time.Since(start).Seconds()

	// Tabel hasil
	fmt.Println("\nHASIL RUNNING TIME")
	fmt.Printf("%-15s %-15s %-15s %-15s\n", "Pendekatan", "Waktu Eksekusi", "Jumlah Tebakan", "Jumlah Data")
	fmt.Println(strings.Repeat("-", 60))
	fmt.Printf("%-15s %-15.6f %-15d %-15d\n", "Iteratif", durationIterative, attemptsIterative, len(guesses))
	fmt.Printf("%-15s %-15.6f %-15d %-15d\n", "Rekursif", durationRecursive, attemptsRecursive, len(guesses))
}
```
