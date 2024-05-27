# code

# widget grafico editable

```
LEFT = widgets.IntSlider(
    value=10,
    min=1,
    max=100,
    step=1,
    description='Trimm left:',
    disabled=False,
    continuous_update=False,
    orientation='horizontal',
    readout=True,
    readout_format='d', layout=Layout(width = '500px', height='30px'))
LEFT.style.handle_color = 'red'
RIGHT = widgets.IntSlider(
    value=10,
    min=1,
    max=100,
    step=1,
    description='Trimm right:',
    disabled=False,
    continuous_update=False,
    orientation='horizontal',
    readout=True,
    readout_format='d', layout=Layout(width = '500px',
                                      height='30px'))
RIGHT.style.handle_color = 'red'
TRIMM = widgets.ToggleButton(
    value=False,
    description='Trimm',
    disabled=False,
    button_style='', # 'success', 'info', 'warning', 'danger' or ''
    tooltip='Description',
    icon='check' # (FontAwesome names without the `fa-` prefix)
)
SALVAR = widgets.ToggleButton(
    value=False,
    description='Save',
    disabled=False,
    button_style='', # 'success', 'info', 'warning', 'danger' or ''
    tooltip='Description',
    icon='check' # (FontAwesome names without the `fa-` prefix)
)
secF = Trace('descargas/cepa2-f-tubF.ab1')

#

def f(LEFT, RIGHT, TRIMM, SALVAR):
    
    fig = plt.figure(figsize =(10, 3))

    ax = fig.add_axes([0, 0, 1, 1])
    ax.set_ylim(0, 70)
    ax.set_xlim(-5, len(secF.seq) + 5)

    ax.plot(range(len(secF.qual_val)), secF.qual_val, lw = 1,
            color = 'black', alpha = 0.7, linestyle = '--')
    ax.plot([0, len(secF.seq) + 5], [20, 20], color = 'silver', linestyle = '--', lw = 1, zorder = 0)
    if TRIMM == True:
        new = secF.qual_val[LEFT:][:-RIGHT]
        ax.plot(range(LEFT, len(new) + LEFT), new, lw = 5,
                color = 'salmon', alpha = 0.5)
    plt.close()
    display(fig)
    if SALVAR == True:
        s = open(secF.id+'_trimm.fasta', 'w')
        s.write('>'+secF.id+'\n'+secF.seq[LEFT:][:-RIGHT])
        s.close()
        
out = widgets.interactive_output(f, {'LEFT': LEFT,
                                     'RIGHT': RIGHT,
                                     'TRIMM': TRIMM,
                                     'SALVAR': SALVAR})
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
