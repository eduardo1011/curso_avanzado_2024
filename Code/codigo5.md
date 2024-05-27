# code

# widget grafico editable

```
def f(LEFT, RIGHT, TRIMM):
    
    fig = plt.figure(figsize =(10, 3))

    ax = fig.add_axes([0, 0, 1, 1])
    ax.set_ylim(0, 70)
    ax.set_xlim(-5, len(secuencia.seq) + 5)

    ax.plot(range(len(secuencia.qual_val)), secuencia.qual_val, lw = 1,
            color = 'black', alpha = 0.7, linestyle = '--')
    ax.plot([0, len(secuencia.seq) + 5], [20, 20], color = 'silver', linestyle = '--', lw = 1, zorder = 0)
    if TRIMM == True:
        new = secuencia.qual_val[LEFT:][:-RIGHT]
        ax.plot(range(LEFT, len(new) + LEFT), new, lw = 5,
                color = 'salmon', alpha = 0.5)
    plt.close()
    display(fig)
    
out = widgets.interactive_output(f, {'LEFT': LEFT, 'RIGHT': RIGHT, 'TRIMM': TRIMM})
```

# -------------

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
