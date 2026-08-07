# RESULTS (RECONSIDERED):
reconsidered results (after fixing the mistake with the negative edges):

# I.
Epochs 201, dropout 0.2, lr = 0.003, dacay 1e-5 - initial configuration:
GCN test CEL: 0.46302294731140137, GCN test accuracy: 0.786300003528595
RGCN test CEL: 0.42737793922424316, RGCN test accuracy: 0.803974986076355


# II.
Let's experiment with epochs:
Epochs X, dropout 0.2, lr = 0.003, dacay 1e-5 - initial configuration:

301
GCN test CEL: 0.4531770944595337, GCN test accuracy: 0.7943500280380249
RGCN test CEL: 0.41338589787483215, RGCN test accuracy: 0.8123250007629395

501
GCN test CEL: 0.4369974732398987, GCN test accuracy: 0.805400013923645
RGCN test CEL: 0.39891788363456726, RGCN test accuracy: 0.8234000205993652

-> choose 501 epochs since it gives the best results


# III.
then experiment with lr:
Epochs 501, dropout 0.2, lr = X, decay 1e-5)

lr 0.01 (epochs 501)
GCN test CEL: 0.4356706440448761, GCN test accuracy: 0.8066250085830688
RGCN test CEL: 0.39323484897613525, RGCN test accuracy: 0.8276500105857849

lr 0.007 (epochs 501)
GCN test CEL: 0.434418648481369, GCN test accuracy: 0.8065249919891357
RGCN test CEL: 0.3881068229675293, RGCN test accuracy: 0.8310999870300293

lr 0.015 (epochs 501)
GCN test CEL: 0.47513559460639954, GCN test accuracy: 0.7799249887466431
RGCN test CEL: 0.393990695476532, RGCN test accuracy: 0.8248500227928162

-> choose lr 0.007, since it gives the best margin for RGCN (not influencing much GCN, though 0.01 rate is a little bit better: 0.8066 (0.01) vs 0.80652 (0.007).


# IV.
then experiment with dropout:
Epochs 501, dropout X, lr = 0.007, decay 1e-5)

dropout 0.0 (lr 0.007, epochs 501):
GCN test CEL: 0.43581685423851013, GCN test accuracy: 0.8061249852180481
RGCN test CEL: 0.4049874544143677, RGCN test accuracy: 0.8260999917984009

dropout 0.5 (lr 0.007, epochs 501):
GCN test CEL: 0.44547364115715027, GCN test accuracy: 0.8009750247001648
RGCN test CEL: 0.41858193278312683, RGCN test accuracy: 0.8084999918937683

Both dropouts degrade both models, hence stay with dropout 0.2


# V.
finally experiment with decay
Epochs 501, dropout X, lr = 0.007, decay X)

decay = 1e-4 (dropout 0.2, lr 0.007, epochs 501)
GCN test CEL: 0.4306219220161438, GCN test accuracy: 0.8083249926567078
RGCN test CEL: 0.3979876935482025, RGCN test accuracy: 0.8243250250816345

decay = 0 (dropout 0.2, lr 0.007, epochs 501):
GCN test CEL: 0.431331992149353, GCN test accuracy: 0.8100000023841858
RGCN test CEL: 0.38821467757225037, RGCN test accuracy: 0.829925000667572

decay = 0 gives boost to GCN.


# VI.
so the best configuration for GCN:
epochs 501, lr 0.007, dropout 0.2, decay 0
# GCN test CEL: 0.4310455024242401, GCN test accuracy: 0.8102999925613403

the best configuration for RGCN
Epochs 501, lr 0.007,  dropout 0.2, decay 1e-5
# RGCN test CEL: 0.3884543776512146, RGCN test accuracy: 0.830299973487854
