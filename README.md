### String Proxy Puzzle

C-style string cannot be used as a template parameter (X<"abc">() won't compile).
</br>It is possible for any C-style string to use it's proxy as a template parameter and reconstruct the compile-time string from it.
Program below demonstrates it. Code can be modified only in the places where `PUZZLE` is.

```C++
// No headers

template <typename T> 
constexpr auto StringProxy()
{
  PUZZLE 
}

static_assert(StringProxy<PUZZLE>() == "StringProxy", "");
                                                           
int main() { return 0; }
```

Quick Answer:

template <typename T>
constexpr auto StringProxy()
{
	struct Internal
	{
		constexpr bool operator==(const char* value)
		{
			return     
				   value[0] == 'S' 
				&& value[1] == 't'
				&& value[2] == 'r'
				&& value[3] == 'i'
				&& value[4] == 'n'
				&& value[5] == 'g'
				&& value[6] == 'P'
				&& value[7] == 'r'
				&& value[8] == 'o'
				&& value[9] == 'x'
				&& value[10] == 'y';
		}
	};

	return Internal{};
}

static_assert(StringProxy<decltype(StringProxy<int>())>() == "StringProxy", "");
static_assert(!(StringProxy<decltype(StringProxy<int>())>() == "ProxyString"), "");

int main(){	return 0;}
