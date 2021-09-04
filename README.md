
package main

import "fmt"

const (
       winter = 1
       summer = 3
       yearly = winter + summer
)

func main() {
       // var books [4]string
       // var books [1 + 3]string
       var books [yearly]string

       books[0] = "Kafka's Revenge"
       books[1] = "Stay Golden"
       books[2] = "Everythingship"
       books[3] += books[0] + " 2nd Edition"


       // Go compiler can catch indexing errors when constant is used
       // books[4] = "Neverland"

       // Go compiler cannot catch indexing errors when non-constant is used
       // i := 4
       // books[i] = "Neverland"

       // --------------------
       // PRINTING ARRAYS
       // --------------------

       // print the type
       fmt.Printf("books  : %T\n", books)

       // print the elements
       fmt.Println("books  :", books)

       // print the elements in quoted string
       fmt.Printf("books  : %q\n", books)

       // print the elements along with their types
       fmt.Printf("books  : %#v\n", books)
}
package main

import (
	"fmt"
	"strconv"
)

func main() {
	local := 10
	show(local)

	incrWrong(local)
	fmt.Printf("local → %d\n", local)

	// incr(local)
	local = incr(local)
	show(local)

	local = incrBy(local, 5)
	show(local)

	_, err := incrByStr(local, "TWO")
	if err != nil {
		fmt.Printf("err   → %s\n", err)
	}

	local, _ = incrByStr(local, "2")
	show(local)

	// CHAINING

	// can't save the number back into main's local
	show(incrBy(local, 2))
	show(local)

	// can't pass the results of the multiple-value returning func
	// show(incrByStr(local, "3"))

	// can call showErr directly because it accepts the same types
	// of parameters as with incrByStr's result values.
	// local = sanitize(incrByStr(local, "NOPE"))
	// show(local)

	local = sanitize(incrByStr(local, "2"))
	show(local)

	local = limit(incrBy(local, 5), 2000)
	show(local)
}

func show(n int) {
	// can't access main's local
	// fmt.Printf("show : n = %d\n", local)
	fmt.Printf("show  → n = %d\n", n)
}

// wrong: incr can't access to main's `local`
func incrWrong(n int) {
	// n := local
	n++
	// can't return (there are no result values)
	// return n
}

func incr(n int) int {
	n++
	return n
}

func incrBy(n, factor int) int {
	return n * factor
}

func incrByStr(n int, factor string) (int, error) {
	m, err := strconv.Atoi(factor)
	n = incrBy(n, m)
	return n, err
}

func sanitize(n int, err error) int {
	if err != nil {
		return 0
	}
	return n
}

func limit(n, lim int) (m int) {
	// var m int
	m = n
	if m >= lim {
		m = lim
	}
	// return m
	return
}
package main
 
import (
	"fmt"
)
 
func main() {
	local := 10
	show(local)
 
	incrWrong(local)
	fmt.Printf("main -> local = %d\n", local)
}
 
func show(n int) {
	fmt.Printf("show -> n = %d\n", n)
}
 
func incrWrong(n int) {
 
	// n:= main's local variable's value
	n++
}
package main

import (
	"fmt"
	"strconv"
)

func main() {
	local := 10
	show(local)

	incrWrong(local)
	fmt.Printf("local → %d\n", local)

	// incr(local)
	local = incr(local)
	show(local)

	local = incrBy(local, 5)
	show(local)

	_, err := incrByStr(local, "TWO")
	if err != nil {
		fmt.Printf("err   → %s\n", err)
	}

	local, _ = incrByStr(local, "2")
	show(local)

	// CHAINING

	// can't save the number back into main's local
	show(incrBy(local, 2))
	show(local)

	// can't pass the results of the multiple-value returning func
	// show(incrByStr(local, "3"))

	// can call showErr directly because it accepts the same types
	// of parameters as with incrByStr's result values.
	// local = sanitize(incrByStr(local, "NOPE"))
	// show(local)

	local = sanitize(incrByStr(local, "2"))
	show(local)

	local = limit(incrBy(local, 5), 2000)
	show(local)
}

func show(n int) {
	// can't access main's local
	// fmt.Printf("show : n = %d\n", local)
	fmt.Printf("show  → n = %d\n", n)
}

// wrong: incr can't access to main's `local`
func incrWrong(n int) {
	// n := local
	n++
	// can't return (there are no result values)
	// return n
}

func incr(n int) int {
	n++
	return n
}

func incrBy(n, factor int) int {
	return n * factor
}

func incrByStr(n int, factor string) (int, error) {
	m, err := strconv.Atoi(factor)
	n = incrBy(n, m)
	return n, err
}

func sanitize(n int, err error) int {
	if err != nil {
		return 0
	}
	return n
}

func limit(n, lim int) (m int) {
	// var m int
	m = n
	if m >= lim {
		m = lim
	}
	// return m
	return
}

package main 
 
import "fmt"
 
func greeting() {
 
fmt.Println("hello world")
}
 
func main() {
 
greeting()
}
	
package main
 
import "fmt"
 
func average(sf ...float64) float64 {
	total := 0.0
	for _, v := range sf {
		total += v
	}
	return total / float64(len(sf))
}
 
func main() {
	n := average(43, 56, 87, 12, 45, 57)
	fmt.Println(n)
}
package main
 
import "fmt"
 
func average(sf ...float64) float64 {
	total := 0.0
	for _, v := range sf {
		total += v
	}
	return total / float64(len(sf))
}
 
func main() {
	data := []float64{43, 56, 87, 12, 45, 57}
	n := average(data...)
	fmt.Println(n)
}

package main
 
import "fmt"
 
func max(numbers ...int) int {
	var largest int
	for _, v := range numbers {
		if v > largest {
			largest = v
		}
	}
	return largest
}
 
func main() {
	greatest := max(4, 7, 9, 123, 543, 23, 435, 53, 125)
	fmt.Println(greatest)
}

package main

import "fmt"

func main() {

	greeting := func() {

		fmt.Println("hello world")
	}
	greeting()
}

package main 
 
import "fmt"
 
func main() {
 
half := func(n int ) ( int , bool) {
     return n/2 , n%2 == 0 
}
  fmt.Println(half(2))
}

package main

import "fmt"

func main() {

	add := func(x, y int) int {
		return x + y
	}
	fmt.Println(add(1, 4))
}

package main 
import "fmt"
 
func main() {
 
x := 0 
 increment := func() int {
    x++ 
    return x 
 }
 
 fmt.Println(increment())
 fmt.Println(increment())
}
// scope of x is func main 
// func incremet has access to x 

package main

import "fmt"

func makeEvenGenerator() func() int {

	i := 0
	return func() int {
		i += 2
		return i
	}
}

func main() {

	nextEven := makeEvenGenerator()
	fmt.Println(nextEven()) //2
	fmt.Println(nextEven()) //4
	fmt.Println(nextEven()) //6

	masEven := makeEvenGenerator()
	fmt.Println(masEven()) //2
	fmt.Println(masEven()) //4
	fmt.Println(masEven()) //6
}


package main
 
import "fmt"
 
func visit(numbers []int, callback func(int)) {
 
	for _, n := range numbers {
 
		callback(n)
	}
}
 
func main() {
 
	visit([]int{1, 2, 3, 4}, func(n int) {
 
		fmt.Println(n)
	})
}

package main

import "fmt"

func hello() {
	fmt.Print("hello")
}

func world() {

	fmt.Println("world")
}

func main() {

	defer world()
	hello()
}

package main
 
import "fmt"
 
func average(sf ...float64) float64 {
	total := 0.0
	for _, v := range sf {
		total += v
	}
	return total / float64(len(sf))
}
 
func main() {
	data := []float64{43, 56, 87, 12, 45, 57}
	n := average(data...)
	fmt.Println(n)
}
