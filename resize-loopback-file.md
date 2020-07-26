### Resize loop back image 

du -m loop-back-image.img
-> 300

Meaning its 300 mb in size. Now to resize we simply append zeroes to the end of fs
and then resize it. 

`dd if=/dev/zero of=loop-back-image.img bs=1M seek=300 count=100`

`seek=300` : Means "seek" to 300th mb
`count=100` : Means add 100 of 1Mb resulting a total size of 400mb

Now we run resize2fs on it. 

`resizee2fs loop-back-image.img`

To shrink one can do almost similar stuff: 

`dd if=/dev/zero of=loop-back-image.img bs=1M seek=200 count=0`

