# Partner A

## Lucky!
* Do you consider yourself to be a lucky or unlucky person?

## Out of place numbers
You are given an almost sorted array of length k.  Write a function that will return the number of out of place elements that can be removed while leaving only the sorted array leftover.  Elements can only be taken out of the array one at a time and the leftover array must remain sorted each time you take an element out.  If taking an element out would cause the array to be unsorted than you may not remove that element.  If no elements can be removed than return 0.

```ruby
def outOfPlaceChecker(arr)
    out_of_place = false
    i = 0

    while i < arr.length-1
      if arr[i] > arr[i+1] && out_of_place == true
        return nil
      end

      if arr[i] > arr[i+1]
        out_of_place = true

        if arr[i + 2] && arr[i + 2] > arr[i]
          out_of_place_value = 2
        else
          out_of_place_value = 1
        end
      end

      i+=1
    end

    if out_of_place
      return out_of_place_value
    end

    return arr.length
end

outOfPlaceChecker([2,1,3,4])
```
