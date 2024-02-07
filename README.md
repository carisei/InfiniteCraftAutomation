# InfiniteCraftAutomation

Saw https://neal.fun/infinite-craft/.

Automated it in C# because I can. Find below the javascript version if you just want to quickly do this in a browser.

## Javascript version
**Febuary 7, 2024**

- Fixed an issue where firstElement and secondElement would begin to increment to 11, 111, 1111, ad infinitum.

- Changed variables for firstElement and secondElement from let to var allowing them to be manually set once script is running.

```
let maxElementReachedForElement = {};
let totalElements = 0;
var firstElement = 0;
var secondElement = 0;

setInterval(function() {
		document.getElementsByClassName('mobile-item')[firstElement].getElementsByClassName('item')[0].click();
		document.getElementsByClassName('mobile-item')[secondElement].getElementsByClassName('item')[0].click();
		totalElements = document.getElementsByClassName('mobile-item').length;

		secondElement = (++secondElement) % totalElements;

		if (secondElement === 0) {
			maxElementReachedForElement[firstElement] = totalElements;	
			if (Object.keys(maxElementReachedForElement).some(item => maxElementReachedForElement[item] < totalElements)) {
				let prevStart = Object.keys(maxElementReachedForElement).find(item => maxElementReachedForElement[item] < totalElements);
				firstElement = prevStart;
				secondElement = maxElementReachedForElement[prevStart]; // Start from previous end
			} else {
				firstElement = (++firstElement) % totalElements;
				secondElement = firstElement; // No need to repeat the previous combinations.
			}
		}

		document.title = firstElement + '+' + secondElement + '|' + totalElements;
}, 500); // TODO : Find a way other than delay
```
