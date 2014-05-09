---
layout: default
title: newspeak
---

~~~
The programming language NewSpeak? is a language designed 
P. Mukherjee, "A Semantics for NewSpeak? in VDM-SL". In 
I.F. Currie, "NewSpeak - a reliable programming language". 
~~~
###newspeak.vdmsl

{% raw %}
~~~
values
beta:nat1 = 2;
zerot:Time = mk_(0,0);
types
Errvalue = <err>;
Id = token;
Flavdom = set of Fl_elt;
Fl_elt::label : token | <phi>
Tr:: val: bool
TrType:: range: set of bool
EqOp = <EQ> | <NEQ>;
Int::val : int
IntType:: rep : <byte> | <word>
NumOp ::   <numplus> | <binaryminus> | <nummult> | <numdiv> | <nummod>
CompOp = <numgt> | <numlt> | <numge> | <numle>;
Real::val:real
Floatrng::lower:int
Float::range:set of Floatrng
Void::val:<nil>
VoidType :: Flavdom;
Structure:: val: StructValue
StructValue = seq1 of Component;
Component = int | real | bool;
StructureType :: tps: seq1 of CompType
CompType = TrType | Float | IntType;
Vector::val: VectorValue
VectorValue = seq1 of Tr | seq1 of Real | seq1 of Int | seq1 of Void |
VectorType :: lower: int
Union:: val : UnionValue
UnionValue = Int | Real | Tr | Void;
UnionType :: tps : set of (IntType | Float | TrType | VoidType)
Expressible_type = TrType | Float | IntType | VoidType | VectorType |
Location :: nat;
Expressible_value = Errvalue | Tr | Int | Real | Void | Structure |
Storable_value :: Tr | Real | Int | Void | Vector | Structure | Union;
Store = map Location to Storable_value;
Time = nat * nat;
PState:: sto : Store
Denotable_value = Location | Storable_value | Errvalue |
Env = (map Id to Denotable_value) * Location;
EnvState = (Env * PState) | Errvalue;
EST_value:: val : Expressible_value
EST_Iterate :: expst : EST_value
Param = seq of Expressible_value;
Proc :: Param -> PState -> EST_value;
Formal_elt :: id : Id
Program :: Expression;
Expression :: Operation | InnerLoop | Assignment | Scope |
Operation :: MonOperation | BinaryOperation;
MonOperation :: MonOpMonOperand | VectorOperation | Value;
MonOpMonOperand :: operator : MonOp
MonOp = <numabs> | <unaryminus> | <not> | CompileTimeOp | <odd> |
CompileTimeOp :: <inf> | <sup> | <relonly> | <absonly> | <relerr> |
VectorOperation :: vo : VectorOp
VectorOp = <sum> | <product> | <all> | <some> | <vecmax> | <vecmin> |
Multiple :: op : Operation
ToPart = Upto | Downto;
Upto =  Operation;
Downto = Operation;
BinaryOperation:: left : MonOperation
BinaryOp :: NumOp | CompOp | EqOp | BoolOp | VecBinOp | <replaceflav>;
BoolOp = <and> | <or>;
VecBinOp = <concat>;
Value :: ConstantValue | NamedValue | VectorVal | Sequence | Call | 
ConstantValue :: IntegerDenotation | FloatingDenotation | Ascii_Char |
IntegerDenotation :: int;
FloatingDenotation :: real;
BooleanDenotation :: bool;
Ascii_Char :: char;
Ascii_string :: seq1 of char;
NamedValue :: Id | FlavourExtract | FlavourStrip | VectorExtract |
FlavourExtract :: nv : NamedValue
Flavouring :: seq of Flavour;
Flavour:: name : token
FlavourStrip :: nv:NamedValue
VectorExtract :: named : NamedValue
VectorTrimming :: named : NamedValue
CompileTimeValue :: Operation;
VectorVal :: seq1 of Operation;
Sequence :: seq1 of Expression;
Call :: id : Id
StructureValue :: seq1 of Operation;
Widening :: expr : Expression
Type :: PrimitiveType | StrucType | VecType | FlavouredType | UnionTp |
PrimitiveType :: Number | FloatType | VoidValType;
Number :: rep : <bit> | <byte> | <word>
Range::lower : [CompileTimeValue]
FloatType :: range : seq of Range
VoidValType = Flavouring;
VecType :: range : Range
StrucType :: seq1 of Type;
FlavouredType::fl : Flavouring
UnionTp :: seq1 of Type;
TypeName :: Id;
Conditional :: IfThenOnly | IfThenElse | CaseExpr;
IfThenOnly :: prop : Expression
IfThenElse :: prop : Expression
CaseExpr :: expr : Expression
CaseLimb :: test : Tester
Tester = SkeletonType | StrucTest | NonStrucTest;
SkeletonType :: Type | NumSkel | StrucSkel | FlavSkel | VecSkel |
NumSkel :: ranges : [seq1 of Range]
Errors :: abserr : [CompileTimeValue]
StrucSkel :: seq1 of (SkeletonType | <nil>);
FlavSkel:: skel : SkeletonType
VecSkel :: SkeletonType;
UnionSkel :: seq1 of (FlavouredType | VoidValType | FlavSkel);
StrucTest :: seq1 of (NonStrucTest | <nil>);
NonStrucTest :: id : [Id]
Outlimb = Sequence;
OuterLoop :: OuterIntLoop | OuterVecLoop;
OuterIntLoop :: ovr : OverRange
OverRange :: cnt : LoopId
LoopId = Id;
OuterVecLoop :: ovs : OverVectors
OverVectors :: cnt : [LoopId]
OverVector :: id : Id
InnerLoop :: IntLoop | VecLoop | TimeLoop;
IntLoop :: inc : InnerControl
InnerControl = OverRange | PartialRange;
PartialRange :: cnt : LoopId
VecLoop :: ovs : OverVectors
TimeLoop :: time : TimeInterval
TimeInterval = Range;
Assignment :: NvAssignment | MultAssignment | StrAssignment;
NvAssignment :: dest : Id
MultAssignment :: dest : Id
StrAssignment :: dest : seq1 of Id
Scope :: SimpleScope | PackageScope;
SimpleScope :: decls : seq1 of Declaration
Declaration = ImportDecl | ExportDecl | LetDecl | VarDecl | ProcDec |
ImportDecl :: id : Id
ExportDecl :: id : Id
LetDecl :: SimpleLetDecl | StrucLetDecl;
SimpleLetDecl :: id : Id
StrucLetDecl :: ids : seq1 of Id
VarDecl :: id : Id
ProcDec :: nls : [NonLocals]
NonLocals :: ids : [seq1 of Id]
ProcHeading :: id : Id
Formal :: id : Id
Representation = PrimitiveRep | StrucRep | VecRep| UnionRep |
PrimitiveRep :: NumRep | FloatRep;
NumRep :: rep : <bit> | <byte> | <word>
FloatRep :: range : [seq1 of Range]
StrucRep :: seq1 of Representation;
VecRep :: range : Range
UnionRep :: seq1 of Representation;
FlavouredRep :: fl :Flavouring
TypeDec :: id : Id
PackageScope :: ids : seq1 of Id
GuardedScope :: decls : seq1 of GuardedDeclaration
GuardedDeclaration = Declaration | WhereDecl;
WhereDecl :: type : SkeletonType
Assertion :: expr : Expression
TimedExpression :: TimeTakes | TimeAssertion;
TimeTakes :: expr : Expression
TimeAssertion :: expr : Expression






functions
fl_mult: Flavdom * Flavdom -> Flavdom
fl_div: Flavdom * Flavdom -> Flavdom
phi_remove: Expressible_type -> Expressible_type
tr_eq: Tr * Tr * EqOp -> Expressible_value
tr_and: Tr * Tr -> Expressible_value
tr_or: Tr * Tr -> Expressible_value
tr_not: Tr -> Expressible_value

int_eq: Int * Int * EqOp -> Expressible_value

min: set of real -> real
max: set of real -> real
intbinop: Int * Int * NumOp -> Expressible_value
intplus: Int * Int -> Expressible_value
intbinminus: Int * Int -> Expressible_value
intmult: Int * Int -> Expressible_value
intdiv: Int * Int -> Expressible_value
intmod: Int * Int -> Expressible_value

intmax: Int * Int -> Expressible_value
intmin: Int * Int -> Expressible_value

absint: Int -> Int
intmonminus: Int -> Int
odd: Int -> Tr
intcomp: Int * Int * CompOp -> Expressible_value
ascii : char -> int
float: Int -> Real
real_eq: Real * Real * EqOp -> Expressible_value

absreal: Real -> Real
realmonminus: Real -> Real
realbinop: Real * Real * NumOp -> Expressible_value
realplus:Real * Real -> Expressible_value
realbinminus: Real * Real -> Expressible_value
realmult: Real * Real -> Expressible_value
realdiv: Real * Real -> Expressible_value

realmax: Real * Real -> Expressible_value

realmin: Real * Real -> Expressible_value
discard: Real -> Int
round: Real -> Int
realcomp: Real * Real * CompOp -> Expressible_value
inf: Real -> Real
sup: Real -> Real
absonly: Real -> Real
relonly: Real -> Real
abserr: Real -> Real
relerr: Real -> Real

void_eq: Void * Void * EqOp -> Expressible_value
construct_ev: Component * CompType -> Expressible_value
comp_extract: Structure * Flavdom -> Expressible_value
struc_length:StructureType -> nat
vector_extract: Vector * int -> Expressible_value
vector_subv: VectorValue * int * int -> VectorValue
vector_length: VectorType -> nat
vector_flatten:VectorValue -> VectorValue
vector_sum: VectorValue -> Expressible_value
vector_product: VectorValue -> Expressible_value

vector_all: VectorValue -> Expressible_value
vector_some: VectorValue -> Expressible_value
vector_max: VectorValue -> Expressible_value
vector_min: VectorValue -> Expressible_value
vector_concat: Vector * Vector -> Vector



widen_type: Expressible_value * Expressible_type -> Expressible_value
const_type: Expressible_value -> (Expressible_type | Errvalue)
fleq: Expressible_type * Expressible_type -> bool

replace_flavour: Expressible_type * Flavdom -> (Expressible_type|Errvalue)

lub: Expressible_type * Expressible_type -> (Expressible_type | Errvalue)

trlub : TrType * TrType -> TrType
floatlub: Float * Float -> Float
intlub: IntType * IntType -> (IntType | Errvalue)
vectorlub : VectorType * VectorType -> (VectorType | Errvalue)
struclub: StructureType * StructureType -> (StructureType | Errvalue)
unionlub: UnionType * UnionType -> (UnionType | Errvalue)
seqlub: seq1 of Expressible_type -> (Expressible_type | Errvalue)
setlub : set of Expressible_type -> (Expressible_type | Errvalue)

gt : Expressible_type * Expressible_type -> bool


tleq: Expressible_type * Expressible_type -> bool
next_locn: Location -> Location
access: Location -> Store -> Storable_value
update : Location -> Storable_value -> Store -> Store
multi_update: seq of Location -> seq of Storable_value -> Store -> Store
timeleq : Time * Time -> bool
access_env : Id -> Env -> Denotable_value
update_env : Id -> Denotable_value -> Env -> Env
empty_env: Location -> Env
multi_update_env : seq of (Id * Denotable_value) -> Env -> Env
reserve_locn : Env -> (Location * Env)
instantiate_formals : (seq of Formal_elt) -> Param -> Env -> 
mantissa : Real -> Real
exponent : Real -> Real
tplus : Time * Time -> Time
dtplus : seq of Time -> Time
t_trimming_op:int -> Time 
t_vector_extract: int -> Time
t_vector_concat: int * int -> Time
t_vectorsum: int -> Time
t_vectorproduct: int -> Time
t_vector_all: int -> Time
t_vector_some: int -> Time
t_vector_max: int -> Time
t_vector_min: int -> Time
t_vector_flatten: int -> Time
t_vector_subv: int -> Time
t_multi_update : int -> Time
choose : Expressible_type -> Expressible_value

eval_Program : Program -> Location -> Store -> EST_value
eval_Expression : Expression -> Env -> PState -> EST_value
eval_Operation : Operation -> Env -> PState -> EST_value
eval_MonOperation : MonOperation -> Env -> PState -> EST_value
eval_MonOpMonOperand: MonOpMonOperand -> Env -> PState -> EST_value
eval_Abs : EST_value -> EST_value
eval_MonMinus : EST_value -> EST_value
eval_Not : EST_value -> EST_value
eval_CompileTimeOp : CompileTimeOp -> EST_value -> EST_value
eval_Discard : EST_value -> EST_value
eval_Round : EST_value -> EST_value
eval_Mantissa : EST_value -> EST_value
eval_Exponent : EST_value -> EST_value
eval_Odd : EST_value -> EST_value
eval_Float : EST_value -> EST_value
eval_VectorOperation : VectorOperation -> Env -> PState -> EST_value

eval_VectorMult : EST_value -> Multiple -> Env -> EST_value

eval_VectorSum : EST_value -> EST_value
eval_VectorProduct : EST_value -> EST_value
eval_VectorMax : EST_value -> EST_value
eval_VectorMin : EST_value -> EST_value
eval_VectorAll : EST_value -> EST_value
eval_VectorSome : EST_value -> EST_value
eval_VectorFlatten : EST_value -> EST_value


eval_BinaryOperation: BinaryOperation -> Env -> PState -> EST_value
eval_NumOp : BinaryOperation -> Env -> PState -> EST_value
eval_CompOp : BinaryOperation -> Env -> PState -> EST_value
eval_EqOp : BinaryOperation -> Env -> PState -> EST_value
eval_BoolOp : BinaryOperation -> Env -> PState -> EST_value
eval_Concat : BinaryOperation -> Env -> PState -> EST_value
eval_Value: Value -> Env -> PState -> EST_value
eval_ConstantValue : ConstantValue -> PState -> EST_value
eval_NamedValue : NamedValue -> Env -> PState -> EST_value

eval_Identifier : Id -> Env -> PState -> EST_value
eval_FlavourExtract : FlavourExtract -> Env -> PState -> EST_value

eval_Flavouring : Flavouring -> Flavdom
eval_Flavour : Flavour -> Fl_elt
eval_FlavourStrip : FlavourStrip -> Env -> PState -> EST_value
eval_VectorExtract : VectorExtract -> Env -> PState -> EST_value


eval_VectorTrimming : VectorTrimming -> Env -> PState -> EST_value
eval_CompileTimeValue : CompileTimeValue -> Env -> EST_value
eval_VectorVal : VectorVal -> Env -> PState -> EST_value
eval_StructureValue: StructureValue -> Env -> PState -> EST_value
eval_Sequence : Sequence -> Env -> PState -> EST_value
eval_Call : Call -> Env -> PState -> EST_value
eval_Acts: seq of Operation -> Env -> PState -> seq of EST_value
eval_Widening : Widening -> Env -> PState -> EST_value
eval_Type : Type -> Env -> (Expressible_type | Errvalue)
eval_PrimitiveType : PrimitiveType -> Env -> (Expressible_type | Errvalue)
eval_Number : Number -> Env -> (Expressible_type | Errvalue)
eval_Range : Range -> Env -> (set of int | Errvalue)
eval_FloatType : FloatType -> Env -> (Expressible_type | Errvalue)
eval_VoidValType : VoidValType -> (Env -> (Expressible_type | Errvalue))
eval_StrucType : StrucType -> Env -> (Expressible_type | Errvalue)
eval_VecType : VecType -> (Env -> (Expressible_type | Errvalue))
eval_FlavouredType : FlavouredType -> Env -> (Expressible_type | Errvalue)
eval_UnionTp : UnionTp -> Env -> (Expressible_type | Errvalue)
eval_TypeName : TypeName -> Env -> (Expressible_type | Errvalue)

eval_Scope : Scope -> Env -> PState -> EST_value
eval_SimpleScope : SimpleScope -> Env -> PState -> EST_value
eval_Decls: seq of Declaration -> EnvState -> EnvState 
eval_Declaration : Declaration -> EnvState -> EnvState
eval_ImportDecl : ImportDecl -> EnvState -> EnvState
eval_ExportDecl : ExportDecl -> EnvState -> EnvState
eval_LetDecl : LetDecl -> EnvState -> EnvState
eval_SimpleLetDecl : SimpleLetDecl -> EnvState -> EnvState
eval_StrucLetDecl : StrucLetDecl -> EnvState -> EnvState
eval_VarDecl : VarDecl -> EnvState -> EnvState
eval_ProcDec : ProcDec -> EnvState -> EnvState
eval_NonLocals : NonLocals -> Env -> PState -> EnvState
eval_Formals : seq of Formal -> Env -> seq of Formal_elt
eval_Formal : Formal -> Env -> Formal_elt
eval_Representation : Representation -> Env -> (Expressible_type | Errvalue)
eval_PrimitiveRep : PrimitiveRep -> Env -> (Expressible_type | Errvalue)
eval_NumRep : NumRep -> Env -> (Expressible_type | Errvalue)
eval_FloatRep : FloatRep -> Env -> (Expressible_type | Errvalue)
eval_StrucRep : StrucRep -> Env -> (Expressible_type | Errvalue)
eval_VecRep : VecRep -> Env -> (Expressible_type | Errvalue)
eval_UnionRep : UnionRep -> Env -> (Expressible_type | Errvalue)
eval_FlavouredRep : FlavouredRep -> Env -> (Expressible_type | Errvalue)
eval_TypeDec : TypeDec -> EnvState -> EnvState
eval_PackageScope : PackageScope -> Env -> PState -> EST_value
eval_GuardedScope : GuardedScope -> Env -> PState -> EST_value
eval_GuardedDeclarations : seq1 of GuardedDeclaration -> bool -> Env
eval_GuardedDecl : GuardedDeclaration -> Env -> PState -> ((Env *
eval_WhereDecl : WhereDecl -> Env -> PState -> ((Env * PState * bool) | Errvalue)
eval_Assertion : Assertion -> Env -> PState -> EST_value

eval_Conditional: Conditional -> Env -> PState -> EST_value
eval_IfThenOnly : IfThenOnly -> Env -> PState -> EST_value
eval_IfThenElse : IfThenElse -> Env -> PState -> EST_value
eval_CaseExpr : CaseExpr -> Env -> PState -> EST_value
eval_Limbs : seq1 of CaseLimb -> Expressible_value -> Env -> PState ->
eval_Limb : CaseLimb -> Expressible_value -> Env -> PState ->



eval_Tester : Tester -> Expressible_value -> Env -> PState -> 

eval_SkeletonType : SkeletonType -> Expressible_type -> Env ->
eval_NumSkel : NumSkel -> Expressible_type -> Env -> 
eval_StrucSkel : StrucSkel -> Expressible_type -> Env ->
eval_FlavSkel : FlavSkel -> Expressible_type -> Env ->
eval_VecSkel : VecSkel -> Expressible_type -> Env -> 
eval_UnionSkel : UnionSkel -> Expressible_type -> Env ->
eval_NonStrucTest : NonStrucTest -> Expressible_value -> Env -> PState
eval_StrucTest : StrucTest -> Expressible_value -> Env -> PState ->
eval_Testseq : seq of (NonStrucTest | <nil>) -> seq of Expressible_value 
eval_OuterLoop : OuterLoop -> Env -> PState -> EST_value
eval_OuterIntLoop : OuterIntLoop -> Env -> PState -> EST_value
eval_OuterVecLoop : OuterVecLoop -> Env -> PState -> EST_value
eval_OverVectors : OverVectors -> Env -> PState -> (seq1 of (Id * Vector *
eval_InnerLoop : InnerLoop -> Env -> PState -> EST_value
eval_IntLoop : IntLoop -> Env -> PState -> EST_value
eval_InnerControl : InnerControl -> Env -> PState -> ((Id * seq of
eval_SeqIterate : Sequence -> Env -> EST_Iterate -> EST_Iterate
eval_VecLoop : VecLoop -> Env -> PState -> EST_value
eval_TimeLoop : TimeLoop -> Env -> PState -> EST_value
eval_Assignment : Assignment -> Env -> PState -> EST_value
eval_NvAssignment : NvAssignment -> Env -> PState -> EST_value
eval_MultAssignment : MultAssignment -> Env -> PState -> EST_value
eval_StrAssignment : StrAssignment -> Env -> PState -> EST_value

eval_TimedExpression : TimedExpression -> Env -> PState -> EST_value
eval_TimeTakes : TimeTakes -> Env -> PState -> EST_value
eval_TimeInterval : TimeInterval -> Env -> (Time | Errvalue)
eval_TimeAssertion:TimeAssertion -> Env -> PState -> EST_value
Iterate: (EST_value -> EST_value) * nat -> (EST_value ->
NIterate: (EST_Iterate -> EST_Iterate) * nat -> (EST_Iterate ->






~~~{% endraw %}
