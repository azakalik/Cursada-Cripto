# Secreto perfecto
- En la realidad, no es posible implementar un secreto perfecto de manera eficiente, ya que tendriamos que pasar una clave que tenga la misma longitud que el texto, y ademas la clave tendria que ser totalmente aleatoria
- En vez de secreto perfecto, buscamos conseguir **seguridad computacional**, para lo cual asumimos
	- Adversarios eficientes (con tiempo y recursos razonables)
	- Probabilidad de exito $> 0$ pero despreciable
- $Pr(Priv_{π,A}^{eav}(n=1)) = 0.5$
- Antes pediamos $Pr(Priv_{π,A}^{eav}(n=1)) <= 0.5 + negl()$, con $negl()$ siendo "negligible", osea un valor despreciable.