# code 


## Conocer los elementos de los conjuntos

```
def generate_logics(n_sets):
    """Generate intersection identifiers in binary (0010 etc)"""
    for i in range(1, 2**n_sets):
        yield bin(i)[2:].zfill(n_sets)
def sets(data_sets, fmt="{size}"):
    """Generate petal descriptions for venn diagram based on set sizes"""
    datasets = list(data_sets.values())
    n_sets = len(datasets)
    dataset_union = set.union(*datasets)
    universe_size = len(dataset_union)
    
    bin_term = {}
    for j in [i for i in generate_logics(n_sets)]:
        rr = []
        for e, z in enumerate(j):
            if z == '1':
                rr.append(list(data_sets.keys())[e])
        bin_term[j] = rr
    
    petal_labels = {}
    for logic in bin_term:
        included_sets = [datasets[i] for i in range(n_sets) if logic[i] == "1"]
        excluded_sets = [datasets[i] for i in range(n_sets) if logic[i] == "0"]
        petal_set = ((dataset_union & set.intersection(*included_sets)) - set.union(set(), *excluded_sets))
        petal_labels[logic] = [int(fmt.format(logic=logic, size=len(petal_set), percentage=(100*len(petal_set)/universe_size))), petal_set, bin_term[logic]]
    return petal_labels
```

> --------------------------------------------------------------

## interactions
```
RES = sets(conjuntos)

INTERS = []
for u in list(data.keys()):
    for x in [i for i in RES]:
        if RES[x][2] == [u]:
            INTERS.append([x, RES[x][2], RES[x][0]])
for x in [i for i in RES]:
    if RES[x][0] > 0:
        if x.count('1') > 1:
            INTERS.append([x, RES[x][2], RES[x][0]])
VALINTERS = {i[0]: i[2] for i in INTERS}

conex = []
dots = []
for e, u in enumerate([i[0] for i in INTERS]):
    if u.count('1') == 1:
        dots.append([e, e])
        #print([e, e], u)
    if u.count('1') > 1:
        ww = [x for x, y in enumerate(u) if y == '1']
        #print([e, e], u, ww)
        conex.append([[e, e], [ww[0], ww[-1]]])
        for t in ww:
            dots.append([e, t])
```

## plots
```
# comparable con https://www.chiplot.online/upset_plot.html
fig = plt.figure(figsize=(5, 4))

ax = fig.add_axes([0, 0, 1, 1])

v = venn3_unweighted(ax = ax,subsets=(set_amino1,
                              set_amino2,
                              set_amino3),  
      set_labels=('amino1', 'amino2', 'amino3'),  
      set_colors=("orange", "blue", "red"), alpha=0.7)

v.get_patch_by_id('100').set_alpha(0.2)

for i in generate_logics(3):
    v.get_label_by_id(i).set_text(i)
    v.get_label_by_id(i).set_fontsize(15)
    
v.get_label_by_id('A').set_fontsize(20)
v.get_label_by_id('B').set_fontsize(20)
v.get_label_by_id('C').set_fontsize(20)


ax2 = fig.add_axes([1.15, 0, 1, 1])
v = venn3_unweighted(ax = ax2, subsets=(set_amino1,
                              set_amino2,
                              set_amino3),  
      set_labels=('amino1', 'amino2', 'amino3'),  
      set_colors=("orange", "blue", "red"), alpha=0.7)

v.get_patch_by_id('111').set_alpha(0)

for i in generate_logics(3):
    v.get_label_by_id(i).set_fontsize(15)
    
v.get_label_by_id('A').set_fontsize(20)
v.get_label_by_id('B').set_fontsize(20)
v.get_label_by_id('C').set_fontsize(20)


# --------------------

bar_color = 'black' # '#2b524c'
I = 0
II = 0.6
Y1 = -1.2
punto = 180
AlMa = 0.4
LW = 5

total = fig.add_axes([II+0.01, Y1, 0.45, AlMa])
total.set_facecolor('none')
total.set_ylim(-0.5, len(data) - 0.5)

courses = list(data.keys())
values = list(data.values())
total.barh(courses, values, 0.6, color = 'black', alpha = 1)
#total.invert_xaxis()
total.set_yticks([])

for e, i in enumerate(values):
    total.text(i, e, ' ' + str(i), zorder = 5, color = 'black', ha = 'left', va = 'center', fontsize = 12)

total.spines['right'].set_visible(False)
total.spines['left'].set_visible(False)
total.spines['top'].set_visible(False)

#for t in total.get_xticks()[:-1]:
#    total.plot([t, t], [-0.5, len(data) + 0.5], color = 'grey', linewidth = 1, zorder = 0, alpha = 0.5)

total.set_xticks(total.get_xticks()[:-1])

total.set_xlabel('Set size', size = 13)


#----------------------------------------------------------------

inter = fig.add_axes([I, Y1 + AlMa + 0.01, II, 0.6])
inter.set_facecolor('none')
inter.set_xlim(-0.5, len(VALINTERS) - 0.5)

inter.bar(range(len(VALINTERS)), VALINTERS.values(),  0.6, color = bar_color)

for e, v in enumerate(VALINTERS):
    inter.text(e, VALINTERS[v] + 0.1, str(VALINTERS[v]), ha = 'center', va = 'bottom', zorder = 6, fontsize = 12) 
    inter.text(e+ 0.1, VALINTERS[v], '     ' + v, ha = 'center', va = 'bottom', zorder = 6, fontsize = 12, rotation = 90, color = 'red') 

#for t in inter.get_yticks()[:-1]:
#    inter.plot([-0.5, len(VALINTERS) + 0.5], [t, t], color = 'grey', linewidth = 1, zorder = 0, alpha = 0.5)
    
inter.set_xticks([])

inter.spines['right'].set_visible(False)
inter.spines['top'].set_visible(False)
inter.spines['bottom'].set_visible(False)

inter.set_ylabel('Intersection size', size = 13)

#----------------------------------------------------------------

matrix = fig.add_axes([I, Y1, II, AlMa])
matrix.set_facecolor('none')
matrix.set_ylim(-0.5, len(data) - 0.5)
matrix.set_xlim(-0.5, len(VALINTERS) - 0.5)

N = 0
for y in range(len(data)):
    for x in range(len(VALINTERS)):
        matrix.scatter(x, y, c = 'gainsboro', s = punto, zorder = 5, alpha = 0.7,  lw = 0)
        N += 1

F = 0
for d in conjuntos:
    matrix.text(-0.6, F, d + ' ', ha = 'right', va = 'center', zorder = 7, fontsize = 13)
    F += 1
    
matrix.set_yticks([])
matrix.set_xticks([])

for cx, cy in conex:
    matrix.plot(cx, cy, color = bar_color, linewidth = LW, zorder = 7)
    
for i in dots:
    x, y = i[0], i[1]
    matrix.scatter(x, y, c = bar_color, s = punto, zorder = 8, alpha = 1)

matrix.spines['right'].set_visible(False)
matrix.spines['left'].set_visible(False)
matrix.spines['top'].set_visible(False)
matrix.spines['bottom'].set_visible(False)

for i in range(len(data)):
    if i%2 == 1:
        matrix.plot([-0.5, len(VALINTERS)-0.5], [i, i], color = 'gainsboro', linewidth = punto/7, zorder = 1, alpha = 0.3, solid_capstyle = 'butt')


con = fig.add_axes([1.1, Y1, 1.5, 1])
N = 0.9
for i in RES:
    con.text(0, N, '  '+ i +' = '+ str(RES[i]), fontsize = 13, family = 'monospace')
    N -= 0.1
con.axis('off')
    
plt.close()
fig
```
