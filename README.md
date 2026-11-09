# Trabalho-Faculdade-
 
CREATE TABLE pais(
cod_país int primary key,
nome VARCHAR(50) not null
);
 
CREATE TABLE equipe(
cod_equipe  int primary key,
nome varchar(50) not null,
cod_país int not null,
foreign key (cod_país) references pais(cod_país)
);
 
CREATE TABLE piloto (
    cod_piloto      INT PRIMARY KEY,
    nome            VARCHAR(60) NOT NULL,
    data_nascimento DATE,
    cod_país        INT NOT NULL,
    cod_equipe      INT,
    FOREIGN KEY (cod_país)   REFERENCES pais(cod_país),
    FOREIGN KEY (cod_equipe) REFERENCES equipe(cod_equipe)
);
 
CREATE TABLE gp (
    cod_gp       INT PRIMARY KEY,
    nome         VARCHAR(60) NOT NULL,
    voltas       INT NOT NULL,
    cod_país     INT NOT NULL,
    data_corrida DATE,
    FOREIGN KEY (cod_país) REFERENCES pais(cod_país)
);
 
CREATE TABLE resultado (
    cod_piloto INT NOT NULL,
    cod_gp     INT NOT NULL,
    posicao    INT NOT NULL,
    pontos     INT NOT NULL,
    PRIMARY KEY (cod_piloto, cod_gp),
    FOREIGN KEY (cod_piloto) REFERENCES piloto(cod_piloto),
    FOREIGN KEY (cod_gp)     REFERENCES gp(cod_gp)
);
 
INSERT INTO pais (cod_país, nome) VALUES
(1,'Brasil'),(2,'Itália'),(3,'França'),(4,'Alemanha'),(5,'Reino Unido'),
(6,'Espanha'),(7,'Áustria'),(8,'Suíça'),(9,'Bélgica'),(10,'Mônaco'),(11,'Países Baixos');
 
INSERT INTO equipe (cod_equipe, nome, cod_país) VALUES
(1,'Ferrari',2),(2,'McLaren',5),(3,'Williams',5),(4,'Mercedes',4),
(5,'Alpine',3),(6,'Sauber',8),(7,'Red Bull',7);
 
INSERT INTO equipe (cod_equipe, nome, cod_país) VALUES
(8,'Racing Bulls',2),(9,'Aston Martin',5),(10,'Lotus',5);
 
INSERT INTO piloto (cod_piloto, nome, data_nascimento, cod_país, cod_equipe) VALUES
(1,'Ayrton Senna','1960-03-21',1,2),
(2,'Nelson Piquet','1952-08-17',1,3),
(3,'Emerson Fittipaldi','1946-12-12',1,2),
(4,'Rubens Barrichello','1972-05-23',1,1),
(5,'Felipe Massa','1981-04-25',1,1),
(6,'Gabriel Bortoleto','2004-10-14',1,6),
(7,'Giancarlo Fisichella','1973-01-14',2,5),
(8,'Jarno Trulli','1974-07-13',2,5),
(9,'Kimi Antonelli','2006-08-25',2,4),
(10,'Alain Prost','1955-02-24',3,2),
(11,'Pierre Gasly','1996-02-07',3,5);
 
INSERT INTO piloto (cod_piloto, nome, data_nascimento, cod_país, cod_equipe) VALUES
(12,'Michael Schumacher','1969-01-03',4,1),
(13,'Lewis Hamilton','1985-01-07',5,4),
(14,'Fernando Alonso','1981-07-29',6,5),
(15,'Max Verstappen','1997-09-30',11,7);
 
INSERT INTO gp (cod_gp, nome, voltas, cod_país, data_corrida) VALUES
(1,'GP do Brasil',71,1,'2025-11-09'),
(2,'GP da Itália',53,2,'2025-09-07'),
(3,'GP de Mônaco',78,10,'2025-05-25'),
(4,'GP da Bélgica',44,9,'2025-07-27'),
(5,'GP da Inglaterra',52,5,'2025-07-06'),
(6,'GP da França',53,3,'2018-06-24');
 
INSERT INTO gp (cod_gp, nome, voltas, cod_país, data_corrida) VALUES
(7,'GP da Espanha',66,6,'2025-06-01'),
(8,'GP da Áustria',71,7,'2025-06-29'),
(9,'GP da Alemanha',67,4,'2019-07-28'),
(10,'GP dos Países Baixos',72,11,'2025-08-31');
 
INSERT INTO resultado (cod_piloto, cod_gp, posicao, pontos) VALUES
(1,1,1,25),(2,1,2,18),(4,1,3,15),(5,1,4,12),(13,1,5,10),(15,1,6,8),
(12,2,1,25),(7,2,2,18),(8,2,3,15),(9,2,4,12),(10,2,5,10),(14,2,6,8),
(10,3,1,25),(1,3,2,18),(11,3,3,15),(13,3,4,12),(6,3,5,10),(15,3,6,8),
(15,4,1,25),(13,4,2,18),(14,4,3,15),(3,4,4,12),(5,4,5,10),(9,4,6,8),
(13,5,1,25),(15,5,2,18),(12,5,3,15),(4,5,4,12),(2,5,5,10),(11,5,6,8),
(11,6,1,25),(14,6,2,18),(6,6,3,15),(8,6,4,12),(7,6,5,10),(3,6,6,8);
 
SELECT nome FROM pais WHERE nome LIKE 'B%l';
 
SELECT p.nome
FROM piloto p
JOIN pais c ON c.cod_país = p.cod_país
WHERE c.nome IN ('Brasil','Itália','França');
 
SELECT nome FROM piloto;
 
SELECT nome AS nome_gp, voltas AS qtd_voltas FROM gp;
 
SELECT p.nome AS piloto, c.nome AS pais
FROM piloto p
JOIN pais c ON c.cod_país = p.cod_país;
 
ALTER TABLE piloto ADD COLUMN salario DECIMAL(12,2);
 
UPDATE piloto SET salario =  95000 WHERE cod_piloto = 1;
UPDATE piloto SET salario =  80000 WHERE cod_piloto = 2;
UPDATE piloto SET salario =  70000 WHERE cod_piloto = 3;
UPDATE piloto SET salario =  85000 WHERE cod_piloto = 4;
UPDATE piloto SET salario =  90000 WHERE cod_piloto = 5;
UPDATE piloto SET salario =  60000 WHERE cod_piloto = 6;
UPDATE piloto SET salario =  75000 WHERE cod_piloto = 7;
UPDATE piloto SET salario =  70000 WHERE cod_piloto = 8;
UPDATE piloto SET salario =  65000 WHERE cod_piloto = 9;
UPDATE piloto SET salario = 100000 WHERE cod_piloto = 10;
UPDATE piloto SET salario =  85000 WHERE cod_piloto = 11;
UPDATE piloto SET salario = 120000 WHERE cod_piloto = 12;
UPDATE piloto SET salario = 110000 WHERE cod_piloto = 13;
UPDATE piloto SET salario = 100000 WHERE cod_piloto = 14;
UPDATE piloto SET salario = 130000 WHERE cod_piloto = 15;
 
SELECT nome, salario FROM piloto WHERE salario BETWEEN 70000 AND 100000;
 
SELECT cod_país, AVG(salario) AS media_salarial
FROM piloto
GROUP BY cod_país;
 
SELECT DISTINCT salario FROM piloto ORDER BY salario ASC;

