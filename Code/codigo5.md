# code

```
fig = plt.figure(figsize =(15, 4))

ax = fig.add_axes([0, 0, 1, 1])
ax.set_ylim(0, 70)
ax.set_xlim(-5, len(secF.seq) + 5)

ax.plot(range(len(secF.qual_val)), secF.qual_val, lw = '1', color = 'black',
        alpha = 0.5, linestyle = '--')
ax.plot(range(12, len(st) + 12), st, lw = '3', color = 'red', alpha = 0.5)


plt.close()
fig 
```
