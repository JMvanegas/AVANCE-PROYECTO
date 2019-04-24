create TABLE Cliente
(
idcliente varchar2(10) primary key,
nom_cliente varchar2(100) not null,
ape_cliente varchar2(100) not null,
Dui varchar2(20) not null,
Nit VARCHAR2(20) not null,
sexo varchar2(2),
edad int,
N_Cuenta varchar2(50) not null,
direccion varchar2(100) not null,
telefono varchar(10) not null,
Trabajo varchar(100)
);

create table Registro_Usuario
(
idusuario varchar2(10) primary key,
nom_usuario varchar2(50) not null,
ape_usuario varchar2(50) not null,
usuario varchar2(40) not null,
contraseña varchar2(20) not null,
idcliente varchar2(10),
foreign key(idcliente) references Cliente(idcliente)
);

create table Login
(
idlog varchar(10) primary key,
usuario varchar2(40) not null,
contraseña varchar2(20) not null,
idcliente varchar2(10),
idusuario varchar2(10),
foreign key(idcliente) references Cliente(idcliente),
foreign key(idusuario) references Registro_Usuario(idusuario)
);

create table Cuenta
(
idcuenta varchar2(10) primary key,
N_Cuenta varchar2(50) not null,
Saldo decimal(7,2),
idcliente varchar2(10),
idusuario varchar2(10),
idlog varchar2(10),
foreign key(idcliente) references Cliente(idcliente),
foreign key(idusuario) references Registro_Usuario(idusuario),
foreign key(idlog) REFERENCES Login(idlog)
);

create table TipoCuenta
(
tipo varchar2(30),
descripcion varchar2(100),
idcuenta varchar2(10),
foreign key(idcuenta) references Cuenta(idcuenta)
);

create table Transacciones
(
idtransaccion varchar2(10) primary key,
TipoTransaccion varchar(50) not null,
descripcion varchar(100),
MontoT decimal(7,2)not null,
FechaTransaccion date,
idcliente varchar2(10),
idusuario varchar2(10),
idlog varchar2(10),
idcuenta varchar(10),
foreign key(idcliente) references Cliente(idcliente),
foreign key(idusuario) references Registro_Usuario(idusuario),
foreign key(idlog) REFERENCES Login(idlog),
foreign key(idcuenta) references Cuenta(idcuenta)
);

create table Pagos
(
idpago varchar(10) primary key,
montoP decimal(7,2) not null,
fechaPago date,
idcliente varchar2(10),
idusuario varchar2(10),
idlog varchar2(10),
idcuenta varchar(10),
foreign key(idcliente) references Cliente(idcliente),
foreign key(idusuario) references Registro_Usuario(idusuario),
foreign key(idlog) REFERENCES Login(idlog),
foreign key(idcuenta) references Cuenta(idcuenta)
);

create table TipoPago
(
Tipo_Pago varchar2(30)not null,
descripcion varchar2(100) not null,
idpago VARCHAR2(10) not null,
foreign key(idpago) references Pagos(idpago)
);