def calculate_cost(y_true, y_pred, fp_cost=1, fn_cost=10):
    cm = confusion_matrix(y_true, y_pred)
    tn, fp, fn, tp = cm.ravel()
    total_cost = (fp * fp_cost) + (fn * fn_cost)
    return total_cost

dt_cost = calculate_cost(y_test, dt_preds)
rf_cost = calculate_cost(y_test, rf_preds)

print(f"Total Cost (Decision Tree): {dt_cost}")
print(f"Total Cost (Random Forest): {rf_cost}")
