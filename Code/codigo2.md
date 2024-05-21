# Code

> -----------------------------
# diagramas de Venn

```
from matplotlib_venn import venn2_unweighted
from matplotlib_venn import venn3_unweighted
import matplotlib.pyplot as plt

def generate_logics(n_sets):
    """Generate intersection identifiers in binary (0010 etc)"""
    for i in range(1, 2**n_sets):
        yield bin(i)[2:].zfill(n_sets)
```

## Venn 2 conjuntos
```
plt.figure(figsize=(5, 5))
v = venn2_unweighted(subsets=(set1, set2),
                     set_labels=('set1', 'set1'),
                     set_colors=("orange", 
                             "red"), alpha=0.7)

v.get_patch_by_id('11').set_alpha(0)

v.get_label_by_id('11').set_fontsize(20)
v.get_label_by_id('11').set_fontweight('bold')

v.get_label_by_id('10').set_fontsize(20)
v.get_label_by_id('01').set_fontsize(20)

v.get_label_by_id('A').set_fontsize(20)
v.get_label_by_id('B').set_fontsize(20)

# si quieres salvar el gráfico activa la siguiente línea, y vuelve a correr la celda
#plt.savefig('Conjuntos.png',dpi = 600, bbox_inches='tight')

plt.show()
```

## Venn 3 conjuntos
```
plt.figure(figsize=(5, 5))
v = venn3_unweighted(subsets=(set1, set2, set3),  
      set_labels=('Group A', 'Group B', 'Group C'),  
      set_colors=("orange", "blue", "red"), alpha=0.7)

v.get_patch_by_id('111').set_alpha(0)

for i in generate_logics(3):
    v.get_label_by_id(i).set_fontsize(15)
    
v.get_label_by_id('A').set_fontsize(20)
v.get_label_by_id('B').set_fontsize(20)
v.get_label_by_id('C').set_fontsize(20)

plt.show()
```

```
plt.figure(figsize=(5, 5))
v = venn3_unweighted(subsets=(set1, set2, set3),  
      set_labels=('Group A', 'Group B', 'Group C'),  
      set_colors=("orange", "blue", "red"), alpha=0.7)

v.get_patch_by_id('111').set_alpha(0)

for i in generate_logics(3):
    v.get_label_by_id(i).set_text(i)
    v.get_label_by_id(i).set_fontsize(15)
    
v.get_label_by_id('A').set_fontsize(20)
v.get_label_by_id('B').set_fontsize(20)
v.get_label_by_id('C').set_fontsize(20)

plt.show()
```
