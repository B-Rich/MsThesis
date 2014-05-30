#Code used to generate the adaptive mesh in Fenics
##################################################
# Compute error indicator
      	def F(x,y):
          	return x*100.0+100.0*y
      	gamma = []
      	coordinates = mesh.coordinates()
      	for a in cells(mesh):
          	h = a.diameter()  # h for cell a
          	A = a.volume()  # Area of the cell a
        for cell in mesh.cells():
              	z = coordinates[cell] # return the 3 coordinates of cell
              	F_a = F(z[0][0],z[0][1])
              	F_b = F(z[1][0],z[1][1])
              	F_c = F(z[2][0],z[2][1]) 
              	F_average = (F_a+F_b+F_c)/3.0
              	g = h*F_average*A
              	gamma.append(g)
      	# Compute error estimator
      	E = sqrt(sum([g*g for g in gamma]))
      	# Check for convergence
      	TOL = 0.0000001
      	if E < TOL:
         	break
      	# Mark cells for refinement
      	cell_markers = CellFunction("bool" , mesh)
      	gamma_sorted = sorted(gamma)
      	n = len(gamma_sorted)
      	i = int(0.8*n)
      	gamma_0 = gamma_sorted[i]
      	for c in cells(mesh):
          	if gamma[c.index()] > gamma_0:
              		cell_markers[c] = True
          	else:
              		cell_markers[c] = False
       	# Refine mesh
      	mesh = refine(mesh, cell_markers)     
